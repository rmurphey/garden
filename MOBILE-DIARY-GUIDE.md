# Mobile Garden Diary Guide

A simple guide for recording video garden tours and turning them into detailed diary entries with AI.

## Quick Start

1. **In your garden**: Record a short video (1-5 minutes) narrating what you observe
2. **Upload**: Transfer video to `diary-inbox/YYYY-MM-DD/` folder
3. **Process**: Run `/process-diary` in Claude Code
4. **Review**: Check and edit the generated entry

That's it! AI handles transcription, visual analysis, and formatting.

---

## Recording Your Garden Video

### What to Say

Narrate as you walk through the garden. Talk naturally, like you're giving a friend a tour!

**Start with context:**
- "November 16th, checking on the garden this morning"
- "It's about 65 degrees, sunny"

**For each plant/area:**
- Name the crop/variety: "Here are the Cherokee Purple tomatoes..."
- Describe what you see: "Looking at about 5 ripe fruits, one is getting overripe"
- Note changes: "This has grown a lot since last week"
- Mention problems: "See this yellowing on the lower leaves..."
- Share harvests: "Picked 3 medium tomatoes today"

**End with plans:**
- "Need to plant lettuce this weekend"
- "Should pick up more compost"

### Example Script

> "November 16th, walking through the garden. It's about 65 degrees, nice and sunny.
>
> Starting with the tomatoes. Here's the Cherokee Purple - you can see about 5 fruits that are ready, this one here is getting really ripe, might be overripe tomorrow. Some yellowing on these lower leaves, probably nitrogen deficiency.
>
> Moving to the Early Girl, harvested 3 medium tomatoes from here today. Plant is healthy overall.
>
> Basil over here is still going strong despite the cooler nights. Might harvest some today for pesto.
>
> Peppers are showing some aphids on the leaves here, see these little bugs? Need to deal with that soon.
>
> Plans for next week: plant the fall lettuce in bed 2, and need to get more compost."

---

## Phone Camera Tips

### iPhone

1. Open **Camera** app
2. Select **Video** mode
3. **Hold phone horizontally** (landscape) for better viewing later
4. Tap to focus on plants as needed
5. When done, video saves to Photos app

**Transfer to computer:**
- **AirDrop**: Select video → Share → AirDrop to Mac
- **iCloud Photos**: Syncs automatically if enabled
- **Direct cable**: Connect iPhone → Finder → drag video file

### Android

1. Open **Camera** app
2. Switch to **Video** mode
3. **Hold phone horizontally** (landscape)
4. Tap to focus as needed
5. Video saves to Gallery/Photos

**Transfer to computer:**
- **Google Photos**: Auto-backup if enabled, download from photos.google.com
- **Direct cable**: Connect phone → File Transfer mode → drag video
- **Cloud storage**: Upload to Dropbox/Google Drive, download on computer

---

## Recording Technique

### Lighting
- **Best times**: Morning (8-10am) or late afternoon (4-6pm)
- Avoid harsh midday sun (creates shadows, washed out colors)
- Overcast days give even lighting

### Camera Movement
- **Move slowly** - give AI time to analyze each plant
- **Pause** for 2-3 seconds on important details
- **Get close** for problems, fruits, flowers
- **Show context** - where in the garden you are

### What to Show

✅ **Do show:**
- Overall plant health and size
- Close-ups of fruits/vegetables
- Any problems (pests, disease, damage)
- Plant tags/labels (so AI can read variety names)
- Harvests laid out
- Your hand next to plants (for scale)

❌ **Don't worry about:**
- Perfect cinematography
- Editing or retakes
- Background mess
- Brief shakiness

### Length

**1-5 minutes total is plenty!**
- Quick check-in: 1-2 minutes
- Thorough tour: 3-5 minutes
- Multiple short videos are fine (they'll be combined in one entry)

---

## File Organization

### Folder Structure

```
diary-inbox/
├── 2025-11-16/
│   ├── garden-tour.mp4        (your video)
│   └── harvest-closeup.mp4    (optional second video)
├── 2025-11-17/
│   └── morning-check.mp4
└── 2025-11-18/
    └── problem-aphids.mp4
```

### Naming Videos

Name doesn't matter much, but helpful names help you remember:
- `garden-tour.mp4`
- `tomato-harvest.mp4`
- `aphid-problem.mp4`
- `full-garden-nov-16.MOV`

**Date folder name is what matters**: Use `YYYY-MM-DD` format
- ✅ `2025-11-16`
- ❌ `Nov 16`
- ❌ `11-16-2025`

---

## Processing Your Video

### In Claude Code

1. Upload your video to `diary-inbox/YYYY-MM-DD/`
2. In Claude Code, type: `/process-diary`
3. Enter the date (or "today")
4. Confirm processing
5. AI will:
   - Transcribe your narration
   - Analyze what's shown in the video
   - Identify plants, problems, harvests
   - Read any visible plant tags
   - Fetch weather data
   - Compare to previous entries
   - Generate structured diary entry
6. Review the entry in `diary/YYYY-MM-DD.md`
7. Edit if needed!

### What the AI Extracts

From your video, the AI will identify:

**From your voice:**
- Crops and varieties mentioned
- Observations and problems described
- Tasks completed
- Harvest quantities
- Plans and next steps

**From the visuals:**
- Plant identification (matching to your garden strategy)
- Growth stage and health status
- Fruit/vegetable quantities visible
- Problems visible (pests, disease, stress)
- Text on plant tags/labels
- Size estimates (if scale reference present)

**Combined analysis:**
- Matches what you say to what's shown
- Adds visual details you didn't mention
- Flags discrepancies (e.g., you said 3 but video shows 5)
- Tracks growth vs. previous videos

---

## Pro Tips

### For Better AI Analysis

**Say variety names:**
- "Cherokee Purple tomatoes" > "tomatoes"
- Helps AI match to your garden strategy

**Show plant tags:**
- Pan camera to include tags in frame
- AI can read and extract variety/date info

**Be specific about problems:**
- "Aphids on the pepper leaves" > "some bugs"
- "Yellowing on lower tomato leaves" > "doesn't look great"

**Mention quantities:**
- "About 5 ripe fruits" helps AI verify visual count
- "Harvested 3 medium tomatoes" gives harvest records

### For Growth Tracking

Film the same plants from similar angles each week:
- Stand in roughly same spot
- Same distance from plant
- AI can compare and note growth

Include tags or markers in frame:
- Helps AI identify which plant across weeks
- "Cherokee Purple Bed 1 Plant 2" label is gold

### For Problem Documentation

When showing problems:
1. **Wide shot**: whole plant showing extent
2. **Close-up**: the problem area in detail
3. **Very close**: specific symptoms (leaf spots, bugs)
4. Say it: "This is early blight, see the brown spots..."

---

## Automation (Optional)

You can automate the file sync and processing:

### Option 1: Cloud Sync

**Setup:**
1. Install Dropbox, Google Drive, or iCloud on your computer
2. Create `diary-inbox` folder in synced location
3. Create symbolic link: `ln -s ~/Dropbox/garden-diary-inbox ~/garden/diary-inbox`
4. On phone: upload videos to that cloud folder

**Result:** Videos appear automatically in your garden repo

### Option 2: GitHub Actions

Create an automated workflow (see `AUTOMATION-SETUP.md` for details):
1. Push videos to GitHub
2. GitHub Action automatically runs `/process-diary`
3. Generates entry and commits it
4. You just review and approve

---

## Troubleshooting

### Video won't upload
- **Too large**: Compress using phone settings or HandBrake app
- **Wrong format**: Most phones use .mp4 or .MOV (both work fine)
- **GitHub limit**: Videos over 100MB may need Git LFS

### AI misidentifies plants
- Say variety names clearly in narration
- Make sure plant tags are visible
- Check that plants are listed in your garden strategy file

### Transcription unclear
- Speak clearly (but normal pace is fine)
- Reduce wind noise (mic with hand briefly)
- Background noise is usually OK

### Processing takes too long
- Video length: Keep under 5 minutes for faster processing
- Multiple videos: Process one date at a time
- File size: Compress if very large

---

## Example Workflow: Full Day

**Morning (5 minutes):**
1. Walk to garden with phone
2. Record 2-minute video narrating observations
3. Upload video to Dropbox/Google Drive (auto-syncs)

**Evening (2 minutes):**
1. Open Claude Code on computer
2. Type `/process-diary today`
3. Review generated entry
4. Make any edits
5. Done!

**Time investment:**
- 2 min recording
- 2 min reviewing
- **Total: 4 minutes for a complete diary entry**

Compare to manual entry: 15-20 minutes of typing!

---

## Questions?

**"Can I record multiple videos per day?"**
Yes! Put them all in the same date folder. They'll be combined into one entry.

**"What if I forget to say something?"**
Edit the generated entry afterward! AI does the heavy lifting, you add human touch.

**"Do I need to say everything I see?"**
No! Just narrate highlights. AI will catch visual details you didn't mention.

**"Can family members record too?"**
Absolutely! Anyone can record and upload. Mention your name in video if helpful.

**"What about sensitive info?"**
Don't show/say anything you wouldn't want in a diary. Videos are private, stored locally (unless you share the repo).

**"Can I delete videos after processing?"**
They're automatically moved to `diary/photos/DATE/` for reference. You can delete later if storage is a concern, but keeping them allows re-processing with improved AI later.

---

## Next Steps

1. **Try it:** Record a 1-minute garden tour today
2. **Process it:** Run `/process-diary` and see what happens
3. **Refine:** Try again tomorrow with lessons learned
4. **Make it routine:** Daily/weekly garden videos become effortless diary entries

Happy gardening! 🌱📱🎥
