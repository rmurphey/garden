---
description: Process voice memos and photos into a diary entry using AI
allowed-tools: Read, Write, Bash(date:*), Bash(mv:*), Bash(ls:*), Bash(mkdir:*), WebFetch
model: sonnet
---

# Process Garden Diary from Audio & Photos

Transform voice recordings and photos from the garden into a structured diary entry with AI-powered transcription and image analysis.

## Step 1: Determine Date to Process

Ask the user: "Which date should I process? (Enter date as YYYY-MM-DD, or 'today' for today's date)"

If user says "today", get today's date: !`date +%Y-%m-%d`

Set the DATE variable to the date being processed.

## Step 2: Check for Input Files

Look in `diary-inbox/DATE/` for:
- Video files: `*.mp4`, `*.mov`, `*.m4v`

List what was found: !`ls -lh diary-inbox/DATE/`

If no files found, tell the user: "No files found in diary-inbox/DATE/. Please add video files to that folder first."

If files found, show the user what you found and confirm: "Found X video file(s). Ready to process?"

## Step 3: Fetch Weather Data

Use WebFetch to get weather data for Durham, NC 27707 for the DATE:
- If processing today: get current weather
- If processing past date: get historical weather from Weather Underground or similar
- Extract: temperature, heat index, humidity, conditions

## Step 4: Read Garden Context

Read the current year's garden strategy file (YYYY-garden-strategy.md) to understand:
- What crops are currently planted
- What varieties are being grown
- What stage of the season we're in

This context helps interpret the audio and photos.

## Step 5: Process Video Files

For each video file found in `diary-inbox/DATE/`:

**Use Claude's native video processing capability** (video includes both visual and audio):

**Extract and transcribe the voiceover audio:**
- Transcribe what the user is saying
- Note which crops/areas they're discussing
- Capture observations, problems, tasks, harvests mentioned
- Note any plans or next steps they mention

**Analyze the visual content frame by frame or at key moments:**

1. **Identify plants/crops shown:**
   - What plant/crop is this? (Cross-reference garden strategy for varieties)
   - Match what's shown to what's being discussed in the voiceover
   - Growth stage (seedling, vegetative, flowering, fruiting, mature)
   - Overall health and condition

2. **Look for specific visual details:**
   - Fruits/vegetables visible (type, quantity estimate, ripeness)
   - Flowers (how many, development stage)
   - Signs of problems (yellowing, leaf spots, wilting, pest damage, disease symptoms)
   - Harvest quantities if shown
   - Garden infrastructure (beds, containers, supports)

3. **Read any text visible in frames:**
   - Plant tags with variety names
   - Planting date labels
   - Seed packets
   - Notes or markers in the garden

4. **Estimate measurements when visible:**
   - Plant height/size (if reference objects present)
   - Fruit counts and sizes
   - Affected areas (if showing problems)

**Combine audio + visual analysis:**
- Match voiceover comments to what's shown visually
- Note when visual confirms or adds to verbal observations
- Capture details visible but not mentioned verbally
- Flag any discrepancies (e.g., user says "3 tomatoes" but video shows 5)

**For the video, generate:**
- Timeline of what was shown (if helpful)
- Key observations combining audio + visual
- Problems detected (mentioned or visible)
- Harvests noted or shown

## Step 6: Growth Tracking (Compare to Previous Entries)

If video shows specific plants (especially with visible tags/variety names):

1. Search previous diary entries (look back 1-4 weeks) for videos/photos of the same plant/variety
2. If found, compare and note changes:
   - Growth/size increase
   - New flowers or fruits since last documentation
   - Progression of any problems
   - Overall health trajectory
   - Harvest progression

Include comparison insights like: "Compared to video from Nov 9, this plant has grown approximately 6-8 inches and now has 5+ fruits visible (vs 2 last week)."

## Step 7: Read Historical Weather Context

Reference `durham-historical-weather.md` to compare today's weather to historical norms:
- Is this typical for the date?
- Unseasonably hot/cold?
- Heat index concerns?
- Relevant climate trends?

## Step 8: Extract Key Video Frames (Optional)

If helpful for the diary entry, you can suggest extracting specific frames as still images:
- Frame showing harvest quantities
- Frame clearly showing a problem
- Frame with visible plant tag
- Before/after comparison frames

These can be saved to `diary/photos/DATE/` for inclusion in the entry.

## Step 9: Generate Diary Entry

Combine all the processed information into a structured markdown entry:

```markdown
# Garden Diary - [Full Date]

## Weather
- **Temperature**: [temp]°F
- **Heat Index**: [heat index]°F
- **Humidity**: [humidity]%
- **Conditions**: [conditions]
- **Context**: [comparison to historical norms]

## Summary
[2-3 sentence overview of the day based on audio/photos]

## Crops Observed

### [Crop Name 1]
[Observations from audio and photo analysis combined]
[If photo comparison available: growth changes noted]

### [Crop Name 2]
[Observations from audio and photo analysis combined]

## Tasks Completed
- [Items from audio transcription]

## Problems & Issues
[Any problems mentioned in audio or detected in photos]
[Be specific: which crop, what problem, severity]

## Successes & Harvests
[Harvests mentioned in audio and/or visible in photos with quantities]
[Positive observations from both sources]

## Plans & Next Steps
- [Items mentioned in audio]

## Video & Images

**Original video:** [video-01.mp4](photos/YYYY-MM-DD/video-01.mp4)

[If key frames were extracted, include them:]

![Key moment 1](photos/YYYY-MM-DD/frame-harvest.jpg)
*[Caption: e.g., "Harvested tomatoes: 5 Cherokee Purple, 3 Early Girl"]*

![Key moment 2](photos/YYYY-MM-DD/frame-problem.jpg)
*[Caption: e.g., "Yellow leaves on lower tomato foliage showing interveinal chlorosis"]*

---
*Video processed and analyzed by Claude AI*
*Entry created: [timestamp]*
*Source files: [list of video files processed]*
```

## Step 10: Organize Files

Create the videos/photos directory: !`mkdir -p diary/photos/DATE`

Move processed video files: !`mv diary-inbox/DATE/* diary/photos/DATE/`

This keeps the original video organized by date and accessible for future reference.

## Step 11: Write Diary Entry

Write the generated markdown to `diary/DATE.md`

If an entry already exists for this date:
- Read it first
- Ask user: "A diary entry already exists for this date. Should I: (1) Replace it, (2) Append to it, or (3) Cancel?"
- Proceed based on user choice

## Step 12: Confirm Completion

Tell the user:
- "✅ Diary entry created: diary/DATE.md"
- "🎥 Video(s) organized: diary/photos/DATE/"
- "🤖 Processed X video file(s) - transcribed audio and analyzed visual content"
- "📝 Review the entry and edit if needed - the AI did its best but you know your garden!"

## Tips for Best Video Garden Tours

**Recording tips:**
- Mention the date at the start: "November 16th, checking on the garden..."
- Narrate as you show: "Here are the Cherokee Purple tomatoes, looking at about 5 ripe fruits..."
- Name specific crops and varieties as you show them
- Point out details: "See this yellowing here on the lower leaves..."
- Show scale: include your hand or a familiar object for size reference
- Mention quantities: "Harvested 3 medium tomatoes today"
- Note problems clearly: "Some aphids on these pepper leaves here"
- Share plans: "I'm going to plant lettuce in this bed next week"

**Camera technique:**
- Start with context (which bed/area you're in)
- Move slowly - pause on each plant for a few seconds
- Get close-ups of problems, fruits, flowers
- Show plant tags/labels clearly if present
- Film harvests laid out so quantities are visible
- Use natural lighting (morning or late afternoon is best)
- Hold camera steady or use brief pauses

**For growth tracking:**
- Film from consistent positions for same plants week to week
- Make sure variety names/tags are visible
- Same time of day helps (similar lighting)

**Workflow:**
1. Walk through garden with phone camera recording
2. Narrate what you observe as you go (1-5 minutes total is plenty)
3. Upload video to `diary-inbox/YYYY-MM-DD/` folder
4. Run `/process-diary` command when convenient
5. AI processes video (transcribes audio + analyzes visuals)
6. Review and edit the generated entry as needed

**You can record multiple videos per day** - they'll all be processed together into one cohesive diary entry!
