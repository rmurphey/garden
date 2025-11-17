# Automation Setup Guide

How to set up automated processing of garden diary videos using GitHub Actions.

## Overview

This automation allows you to:
1. Upload videos to the `diary-inbox/` folder
2. Push to GitHub
3. GitHub Actions automatically processes videos with Claude AI
4. Diary entries are generated and committed back to the repo

**Cost:** ~$0.10-0.50 per diary entry (Claude API costs), Free GitHub Actions (2000 min/month)

---

## Prerequisites

- GitHub repository (you have this!)
- Anthropic API key (Claude)
- Videos syncing to `diary-inbox/` folder

---

## Setup Steps

### 1. Get Anthropic API Key

1. Go to https://console.anthropic.com/
2. Sign up or log in
3. Navigate to "API Keys"
4. Click "Create Key"
5. Copy the API key (starts with `sk-ant-...`)

**Cost note:** Claude API pricing (as of 2025):
- Sonnet: ~$3 per million input tokens, ~$15 per million output tokens
- Typical diary video (3 min): ~$0.10-0.50 per processing
- Free tier: $5 credit for new accounts

### 2. Add API Key to GitHub Secrets

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Name: `ANTHROPIC_API_KEY`
5. Value: Paste your API key
6. Click **Add secret**

### 3. Enable GitHub Actions

1. In your repository, go to **Actions** tab
2. If prompted, click **I understand my workflows, go ahead and enable them**
3. You should see the "Process Garden Diary Videos" workflow

### 4. Test the Automation

**Manual test:**
1. Create a test video folder: `diary-inbox/2025-11-16/`
2. Add a short test video
3. Commit and push:
   ```bash
   git add diary-inbox/
   git commit -m "Test: add sample garden video"
   git push
   ```
4. Go to **Actions** tab in GitHub
5. Watch the workflow run
6. Check if `diary/2025-11-16.md` was created

**Manual trigger:**
1. Go to **Actions** tab
2. Select "Process Garden Diary Videos"
3. Click **Run workflow**
4. Enter a date or leave blank for latest
5. Click **Run workflow**

---

## Full Automation Workflow

### Option A: Cloud Sync (Recommended)

**Setup:**

1. **Install cloud storage app:**
   - Dropbox, Google Drive, or iCloud Drive

2. **Create synced folder:**
   ```bash
   # Example with Dropbox
   mkdir -p ~/Dropbox/garden-diary-inbox

   # Create symlink from repo to Dropbox
   ln -s ~/Dropbox/garden-diary-inbox ~/personal/garden/diary-inbox
   ```

3. **Set up auto-commit:**
   Create `.github/workflows/auto-commit-videos.yml`:
   ```yaml
   name: Auto-commit New Videos

   on:
     schedule:
       - cron: '0 20 * * *'  # 8 PM daily
     workflow_dispatch:

   jobs:
     commit-videos:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - name: Commit new videos
           run: |
             git config user.name "Garden Bot"
             git config user.email "bot@garden.local"

             if [ -n "$(git status --porcelain diary-inbox/)" ]; then
               git add diary-inbox/
               git commit -m "Add new garden videos"
               git push
             fi
   ```

**Daily workflow:**
1. Record video on phone
2. Upload to Dropbox/Google Drive `garden-diary-inbox/YYYY-MM-DD/` folder
3. File syncs to your computer automatically
4. At 8 PM: GitHub Action commits new videos
5. Workflow processes videos → generates diary entries
6. Next morning: Review entries, edit if needed

### Option B: Mobile App Upload (Future)

Create a simple web form that:
1. Accepts video upload from phone
2. Organizes by date in diary-inbox
3. Triggers GitHub Action via webhook
4. You receive notification when entry is ready

*(This requires additional setup - see MOBILE-APP-SETUP.md)*

---

## Processing Script

The GitHub Action needs a Python script to actually process videos. Here's the structure:

**Create `scripts/process-diary.py`:**

```python
#!/usr/bin/env python3
"""
Process garden diary videos using Claude AI
"""

import os
import sys
from pathlib import Path
from datetime import datetime
import anthropic

def process_diary_video(date_str, video_path, garden_strategy_path):
    """Process a single video file into a diary entry"""

    client = anthropic.Anthropic(api_key=os.environ.get("ANTHROPIC_API_KEY"))

    # Read garden strategy for context
    with open(garden_strategy_path) as f:
        garden_context = f.read()

    # Process video with Claude
    # Note: This uses Claude's vision + audio capabilities
    with open(video_path, 'rb') as video_file:
        video_data = video_file.read()

    message = client.messages.create(
        model="claude-sonnet-4-5-20250929",
        max_tokens=4096,
        messages=[{
            "role": "user",
            "content": [
                {
                    "type": "document",
                    "source": {
                        "type": "base64",
                        "media_type": "video/mp4",
                        "data": video_data
                    }
                },
                {
                    "type": "text",
                    "text": f"""Process this garden tour video into a diary entry.

Garden context:
{garden_context}

Extract:
1. Transcribe the narration
2. Identify crops shown (match to strategy)
3. Analyze plant health, growth stage
4. Detect any problems (pests, disease, stress)
5. Note harvests visible or mentioned
6. Extract any text from plant tags
7. Generate a detailed diary entry in this format:

# Garden Diary - {date_str}

## Weather
[Fetch weather for Durham, NC 27707 on {date_str}]

## Summary
[2-3 sentence overview]

## Crops Observed
[By crop, combining narration + visual analysis]

## Tasks Completed
[From narration]

## Problems & Issues
[Mentioned or visible]

## Successes & Harvests
[Mentioned or visible with quantities]

## Plans & Next Steps
[From narration]

## Video
[Link to video file]

---
*Processed by Claude AI on {datetime.now().isoformat()}*
"""
                }
            ]
        }]
    )

    return message.content[0].text

def main():
    date = sys.argv[1] if len(sys.argv) > 1 else datetime.now().strftime("%Y-%m-%d")

    inbox_dir = Path(f"diary-inbox/{date}")
    if not inbox_dir.exists():
        print(f"No videos found for {date}")
        return

    # Find video files
    video_files = list(inbox_dir.glob("*.mp4")) + list(inbox_dir.glob("*.mov"))

    if not video_files:
        print(f"No video files in {inbox_dir}")
        return

    # Process each video
    for video_path in video_files:
        print(f"Processing {video_path}...")

        entry = process_diary_video(
            date,
            video_path,
            "2026-garden-strategy.md"  # Adjust year as needed
        )

        # Write diary entry
        diary_path = Path(f"diary/{date}.md")
        diary_path.parent.mkdir(exist_ok=True)

        with open(diary_path, 'w') as f:
            f.write(entry)

        # Move video to photos directory
        photos_dir = Path(f"diary/photos/{date}")
        photos_dir.mkdir(parents=True, exist_ok=True)

        video_dest = photos_dir / video_path.name
        video_path.rename(video_dest)

        print(f"✅ Created {diary_path}")
        print(f"📹 Moved video to {video_dest}")

if __name__ == "__main__":
    main()
```

**Add to GitHub Action** (update `.github/workflows/process-diary-videos.yml`):

Replace the placeholder step with:
```yaml
      - name: Process diary videos
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          python scripts/process-diary.py ${{ steps.find-dates.outputs.dates }}
```

---

## Cost Estimation

### Claude API Costs (Approximate)

**Per 3-minute video:**
- Video processing: ~100K-200K tokens input
- Generated entry: ~2K-5K tokens output
- Cost: **$0.30-0.60 per video**

**Monthly usage scenarios:**

| Frequency | Videos/month | Est. Cost |
|-----------|--------------|-----------|
| Daily | 30 | $9-18 |
| 3x/week | 12 | $3.60-7.20 |
| Weekly | 4 | $1.20-2.40 |

**GitHub Actions:**
- Free tier: 2000 minutes/month
- Typical run: 2-5 minutes
- Videos processed: 400-1000/month (way more than needed!)
- Cost: **$0** (within free tier)

**Total monthly cost:** $1-18 depending on frequency

---

## Troubleshooting

### Workflow fails with "API key not found"
- Check GitHub Secrets: Settings → Secrets → ANTHROPIC_API_KEY exists
- Key should start with `sk-ant-`

### Video files too large
- GitHub has 100MB file limit per file
- Use Git LFS for files > 100MB:
  ```bash
  git lfs install
  git lfs track "*.mp4"
  git lfs track "*.mov"
  git add .gitattributes
  git commit -m "Enable Git LFS for videos"
  ```

### Processing takes too long
- Limit video length to 3-5 minutes
- Process one date at a time
- Use manual trigger instead of auto-trigger

### Generated entries are inaccurate
- Speak clearly in narration
- Show plant tags/labels
- Keep garden strategy file updated
- Edit entries after generation (AI is a tool, not perfect!)

---

## Disabling Automation

If you prefer manual processing:

1. **Disable auto-trigger:**
   - Edit `.github/workflows/process-diary-videos.yml`
   - Remove the `push:` trigger section
   - Keep only `workflow_dispatch` (manual trigger)

2. **Use local processing:**
   - Just use `/process-diary` command in Claude Code
   - No GitHub Actions needed
   - No API costs (uses your Claude Code subscription)

---

## Privacy & Security

**What's uploaded to GitHub:**
- Videos (if repo is private, only you can access)
- Generated diary entries (markdown)
- No API keys (stored securely in GitHub Secrets)

**What's sent to Claude API:**
- Video content
- Garden strategy file (for context)
- Nothing else from your repo

**Keeping it private:**
- Make sure GitHub repo is set to **Private**
- Don't share API keys
- Videos stay in your private repo

**Data retention:**
- Videos stored locally in `diary/photos/DATE/`
- You control what gets committed to GitHub
- Delete videos after processing if desired (entry remains)

---

## Next Steps

1. **Get API key** from Anthropic
2. **Add to GitHub Secrets**
3. **Test with one video**
4. **Set up cloud sync** (optional)
5. **Start recording!**

For questions or issues, refer to the main [MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md).

Happy automating! 🤖🌱
