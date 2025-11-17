# Video Garden Diary System - Overview

A comprehensive system for creating detailed garden diary entries from simple phone videos with AI assistance.

## What You Get

**🎥 Record:** Walk through your garden with phone, narrating what you see (1-5 minutes)

**🤖 Process:** AI transcribes audio, analyzes visuals, identifies plants, reads tags, compares to previous entries

**📝 Result:** Detailed, structured diary entry in markdown with:
- Weather data (auto-fetched)
- Crop observations (from your narration + AI vision)
- Problems identified (you mention + AI spots visually)
- Harvests tracked (quantities, varieties)
- Growth tracking (compares to previous entries)
- Plans documented (from your narration)

---

## System Components

### 1. Commands (`.claude/commands/`)

**`/process-diary`** - Main command
- Processes videos from `diary-inbox/DATE/`
- Transcribes voiceover narration
- Analyzes video frames for plant health, problems, quantities
- Reads plant tags and labels (OCR)
- Fetches weather data for the date
- Compares to previous entries for growth tracking
- Generates structured markdown diary entry
- Moves videos to `diary/photos/DATE/`

**`/diary`** - Original interactive diary (still available)
- Q&A style entry creation
- Good for desktop detailed entries
- No video required

**`/quick-note`** - Fast notes
- Single question: what did you observe?
- Appends to today's diary entry
- Good for brief updates

### 2. Documentation

**[MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md)** - Complete user guide
- How to record effective garden videos
- Phone camera tips (iPhone & Android)
- File organization and upload
- Recording techniques for best AI analysis
- Troubleshooting

**[EXAMPLE-WORKFLOWS.md](EXAMPLE-WORKFLOWS.md)** - Real-world examples
- Daily quick check (5 min)
- Detailed weekend inspection (15 min)
- Problem documentation workflow
- Harvest tracking
- Growth tracking series
- Treatment effectiveness
- Family collaboration
- Season-end reviews

**[AUTOMATION-SETUP.md](AUTOMATION-SETUP.md)** - Optional automation
- GitHub Actions setup
- Anthropic API key configuration
- Cloud sync options (Dropbox/Google Drive)
- Cost estimation (~$1-18/month depending on frequency)
- Python processing script

### 3. Infrastructure

**Folder structure:**
```
diary-inbox/           # Upload videos here
  2025-11-16/
    garden-tour.mp4

diary/                 # Generated entries
  2025-11-16.md
  photos/
    2025-11-16/
      garden-tour.mp4  # Moved after processing
```

**GitHub Action** (`.github/workflows/process-diary-videos.yml`)
- Auto-triggers when videos pushed to repo
- Manual trigger available
- Processes videos → generates entries → commits

---

## How It Works

### The AI Processing Pipeline

1. **Video Input Analysis**
   - Extracts and transcribes audio narration
   - Analyzes visual frames throughout video
   - Combines audio + visual understanding

2. **Context Integration**
   - Reads your garden strategy (what's planted)
   - Fetches weather data for the date
   - References historical weather patterns
   - Looks at previous diary entries

3. **Visual Analysis**
   - Identifies plants (matches to your strategy)
   - Assesses health and growth stage
   - Detects problems (pests, disease, stress)
   - Counts fruits/vegetables visible
   - Reads text from plant tags/labels
   - Estimates measurements

4. **Growth Tracking**
   - Compares to previous videos of same plants
   - Notes changes in size, fruits, health
   - Tracks progression of problems or recovery

5. **Entry Generation**
   - Organizes observations by crop
   - Formats in consistent structure
   - Adds weather context
   - Includes photo references
   - Creates comprehensive summary

---

## Example: What You Do vs What AI Does

### You (2 minutes):

Record video saying:
> "November 16th. Checking the Cherokee Purple tomatoes - about 5 fruits ready, this one's getting overripe. Some yellow leaves down here. Peppers look great after the neem treatment. Harvested 3 tomatoes from Early Girl."

### AI Generates:

```markdown
# Garden Diary - November 16, 2025

## Weather
- Temperature: 58°F
- Heat Index: 56°F
- Humidity: 72%
- Conditions: Partly cloudy
- Context: Typical for mid-November, slightly cooler than average

## Summary
Morning inspection showed Cherokee Purple tomatoes nearing peak ripeness (5 fruits ready, one overripe), ongoing nitrogen deficiency symptoms on lower foliage, successful aphid treatment on pepper plants, and Early Girl harvest of 3 fruits.

## Crops Observed

### Cherokee Purple Tomatoes
- **Fruit Development**: 5 ripe fruits visible, one showing overripeness (splitting risk)
- **Harvest Recommendation**: Pick overripe fruit today
- **Health Issue**: Lower leaves showing interveinal chlorosis consistent with nitrogen deficiency
- **Growth Tracking**: Compared to Nov 9 video, 2 additional fruits have ripened
- **Plant Tag Visible**: "Cherokee Purple, planted 4/15/2025"

### Early Girl Tomatoes
- **Harvest**: 3 medium fruits harvested (approx 1-1.5 lbs total based on visual)
- **Plant Health**: Good overall condition
- **Production**: Steady fruit production continuing

### Peppers
- **Health Status**: Excellent condition post-treatment
- **Pest Control**: Neem oil treatment successful, no aphids visible
- **Visual Analysis**: Foliage healthy, new growth evident
- **Previous Issue Resolved**: Aphid infestation from Nov 13 successfully treated

## Tasks Completed
- Harvested 3 tomatoes from Early Girl
- Inspected all crops
- Monitored pest treatment effectiveness

## Problems & Issues
**Ongoing: Nitrogen Deficiency - Cherokee Purple**
- Interveinal chlorosis on lower 20-30% of foliage
- Progressive issue (visible in last 2 entries)
- Recommendation: Side-dress with compost or dilute nitrogen fertilizer

**Resolved: Aphid Infestation - Peppers**
- Neem treatment from Nov 13 effective
- No new aphid activity observed

## Successes & Harvests
- Early Girl: 3 medium tomatoes (~1-1.5 lbs)
- Cherokee Purple: 5 fruits nearing harvest
- Successful pest management (aphids eliminated)

## Plans & Next Steps
- Harvest overripe Cherokee Purple today
- Address nitrogen deficiency on tomatoes
- Continue monitoring pepper recovery

## Video
**Original video:** [garden-tour.mp4](photos/2025-11-16/garden-tour.mp4)

---
*Video processed and analyzed by Claude AI*
*Entry created: 2025-11-16 08:30:42*
*Source files: garden-tour.mp4 (2:15 duration)*
```

**Your investment:** 2 min recording + 1 min review = 3 minutes total

**AI did:** Transcription, visual analysis, plant ID, problem diagnosis, growth tracking, weather fetching, comparison to history, structured formatting, actionable recommendations

---

## Key Features

### 1. Minimal User Effort
- Just narrate and point camera
- No typing required
- No structured forms
- 2-5 minutes captures detailed observations

### 2. Rich AI Analysis
- Identifies plants automatically
- Spots problems you might miss
- Counts fruits/vegetables
- Reads plant tags/labels
- Provides diagnosis and recommendations

### 3. Growth Tracking
- Compares same plants week-over-week
- Quantifies growth progress
- Tracks problem progression or resolution
- Helps optimize future seasons

### 4. Flexible Usage
- Quick daily checks (1-2 min)
- Detailed weekly tours (5 min)
- Problem-specific documentation
- Harvest recording
- Experiment tracking
- Family collaboration

### 5. Structured Output
- Consistent markdown format
- Organized by crop
- Weather context included
- Searchable and indexed
- Future reference ready

---

## Use Cases

### Daily Gardening
- Quick morning checks before work
- Evening harvest documentation
- Problem spotting and tracking

### Learning & Improvement
- Track what works and doesn't
- Compare varieties performance
- Document experiments
- Build knowledge base

### Planning
- End-of-season reviews for next year
- Variety selection based on performance
- Timing adjustments from observations

### Sharing
- Show progress to family/friends
- Document gifts to neighbors
- Share techniques that work

### Problem Solving
- Document problems with timeline
- Track treatment effectiveness
- Reference Durham-specific solutions

---

## Getting Started

### Immediate (5 minutes):
1. Record a 1-2 min garden video today on your phone
2. Upload to `diary-inbox/YYYY-MM-DD/` folder
3. Open Claude Code, run `/process-diary`
4. Review the generated entry

### This Week:
1. Read [MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md) for tips
2. Try 2-3 different recording styles
3. Review [EXAMPLE-WORKFLOWS.md](EXAMPLE-WORKFLOWS.md) for ideas
4. Pick your preferred workflow

### Optional (Setup once):
1. Set up cloud sync (Dropbox/Google Drive)
2. Configure GitHub Actions automation
3. Add family members

---

## Cost & Requirements

### Required:
- Claude Code subscription (you have this)
- Phone with camera and mic (any smartphone)
- 5-10 min per week

### Optional:
- Anthropic API key for automation (~$1-18/month)
- Cloud storage (free tiers available)
- GitHub Actions (free tier: 2000 min/month)

### Storage:
- ~100-500 MB per video (1-5 minutes)
- ~50-250 GB per year if recording daily
- Less if recording weekly
- Can delete videos after processing (entries remain)

---

## Advantages Over Manual Entry

| Manual Typing | Video + AI |
|--------------|------------|
| 15-20 min per entry | 2-5 min per entry |
| Requires remembering details | Captured in real-time |
| Hard to quantify observations | AI counts and measures |
| Miss subtle problems | AI vision spots issues |
| No growth tracking | Automatic comparisons |
| Desktop-bound | Phone in garden |
| Tedious | Natural and quick |

---

## What Makes This Special

### 1. Context-Aware
The AI knows:
- What you have planted (from strategy file)
- Durham's climate patterns
- Historical weather norms
- Previous diary entries
- Your past successes and challenges

### 2. Vision + Voice
Not just transcription:
- Sees what you point at
- Identifies plants visually
- Spots problems you mention AND ones you don't
- Reads text from tags/labels
- Estimates quantities

### 3. Durham-Specific
- Weather data for Durham, NC 27707
- Climate change context
- Humid heat stress awareness
- Local variety performance

### 4. Learning System
Each entry:
- Builds historical record
- Informs future recommendations
- Tracks experiments
- Documents what works in YOUR garden

---

## Future Enhancements (Potential)

- Photo frame extraction from video (key moments as stills)
- Automated plant problem diagnosis with treatment suggestions
- Harvest quantity tracking and charts
- Variety performance comparisons across seasons
- Automated monthly/seasonal summaries
- Multi-language narration support
- Voice commands for specific observations

---

## Support Documents

| Document | Purpose |
|----------|---------|
| [MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md) | How to record videos, upload, process |
| [EXAMPLE-WORKFLOWS.md](EXAMPLE-WORKFLOWS.md) | Real scenarios and examples |
| [AUTOMATION-SETUP.md](AUTOMATION-SETUP.md) | GitHub Actions automation |
| [README.md](README.md) | Main repository overview |

---

## Quick Reference

### Commands
- `/process-diary` - Process videos
- `/diary` - Interactive entry
- `/quick-note` - Fast note

### Folders
- `diary-inbox/YYYY-MM-DD/` - Upload videos here
- `diary/YYYY-MM-DD.md` - Generated entries
- `diary/photos/YYYY-MM-DD/` - Processed videos

### Video Tips
- Mention date at start
- Name crops as you show them
- Point at details while describing
- Show plant tags
- 1-5 minutes is perfect

### Processing
1. Upload video to dated folder
2. Run `/process-diary`
3. Review and edit entry
4. Done!

---

**Questions?** See [MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md) for detailed help.

**Ready?** Record your first video today! 🎥🌱
