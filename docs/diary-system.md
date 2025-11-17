# Garden Diary System

A comprehensive system for creating detailed garden diary entries from simple phone videos with AI assistance.

## Quick Start

1. **Record**: Walk through your garden with phone, narrating what you see (1-5 minutes)
2. **Upload**: Transfer video to `diary-inbox/YYYY-MM-DD/` folder
3. **Process**: Run `/process-diary` in Claude Code
4. **Review**: Check and edit the generated entry

That's it! AI handles transcription, visual analysis, and formatting.

---

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

## Available Commands

**`/process-diary`** - Main video processing command
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

## How the AI Processing Works

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

### What the AI Extracts

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

## Common Use Cases

### Daily Quick Check
- 1-2 minute video before work
- Quick narration of key observations
- Process later in evening

### Detailed Weekend Inspection
- 5-minute comprehensive video tour
- Show each bed systematically
- Close-ups of any problems
- Film harvests laid out

### Problem Documentation
- Focused video of the specific problem
- Close-up of pests/disease
- Mention treatment plan
- Follow-up videos to track resolution

### Harvest Recording
- Lay out produce organized by type
- Pan over harvest while mentioning quantities
- Perfect for tracking productivity over time

### Growth Tracking Series
- Film same plants from same position each week
- Same time of day for consistent lighting
- AI automatically compares week-over-week

### Experiment Tracking
- Document setup, progress, and results
- Control groups vs test groups
- Before/during/after comparisons

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

### Cloud Sync Option

**Setup:**
1. Install Dropbox, Google Drive, or iCloud on your computer
2. Create `diary-inbox` folder in synced location
3. Create symbolic link from repo to cloud folder
4. On phone: upload videos to that cloud folder

**Result:** Videos appear automatically in your garden repo

### GitHub Actions Automation

Create an automated workflow that:
1. Watches for videos pushed to GitHub
2. Automatically runs video processing with Claude API
3. Generates entry and commits it back
4. You just review and approve

**Cost:** ~$0.10-0.50 per diary entry (Claude API costs), Free GitHub Actions (2000 min/month)

**Setup details:**
- Requires Anthropic API key
- Configuration in `.github/workflows/process-diary-videos.yml`
- Python processing script needed
- See full automation guide below for details

#### Setting Up GitHub Actions

1. **Get Anthropic API Key:**
   - Go to https://console.anthropic.com/
   - Create API key (starts with `sk-ant-...`)

2. **Add to GitHub Secrets:**
   - Repository → Settings → Secrets and variables → Actions
   - New repository secret: `ANTHROPIC_API_KEY`

3. **Enable GitHub Actions:**
   - Go to Actions tab in repository
   - Enable workflows

4. **Test:**
   - Upload test video to `diary-inbox/`
   - Push to GitHub
   - Watch Actions tab for processing

**Monthly cost estimate:**

| Frequency | Videos/month | Est. Cost |
|-----------|--------------|-----------|
| Daily | 30 | $9-18 |
| 3x/week | 12 | $3.60-7.20 |
| Weekly | 4 | $1.20-2.40 |

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

## Questions?

**"Can I record multiple videos per day?"**
Yes! Put them all in the same date folder. They'll be combined into one entry.

**"What if I forget to say something?"**
Edit the generated entry afterward! AI does the heavy lifting, you add human touch.

**"Do I need to say everything I see?"**
No! Just narrate highlights. AI will catch visual details you didn't mention.

**"Can family members record too?"**
Absolutely! Anyone can record and upload. Mention your name in video if helpful.

**"Can I delete videos after processing?"**
They're automatically moved to `diary/photos/DATE/` for reference. You can delete later if storage is a concern.

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

### Context-Aware
The AI knows:
- What you have planted (from strategy file)
- Durham's climate patterns
- Historical weather norms
- Previous diary entries
- Your past successes and challenges

### Vision + Voice
Not just transcription:
- Sees what you point at
- Identifies plants visually
- Spots problems you mention AND ones you don't
- Reads text from tags/labels
- Estimates quantities

### Durham-Specific
- Weather data for Durham, NC 27707
- Climate change context
- Humid heat stress awareness
- Local variety performance

### Learning System
Each entry:
- Builds historical record
- Informs future recommendations
- Tracks experiments
- Documents what works in YOUR garden

---

## Related Documentation

- [Mobile Guide](mobile-guide.md) - Quick reference for phone recording
- [Main README](../README.md) - Repository overview
- Garden strategy files in `planning/`
