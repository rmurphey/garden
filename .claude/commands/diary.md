---
description: Create an interactive garden diary entry with auto-fetched weather data
allowed-tools: Write, Read, Bash(date:*), Bash(mkdir:*), WebFetch
model: sonnet
---

# Garden Diary Entry

Create a comprehensive garden diary entry for today with automatically fetched weather data.

## Step 1: Get Current Information

Get today's date: !`date +%Y-%m-%d`

Fetch current weather for Durham, NC 27707 using WebFetch to get temperature, humidity, heat index, and current conditions.

## Step 2: Read Garden Context

Read the current year's garden strategy file (look for YYYY-garden-strategy.md where YYYY is current year) to understand:
- What crops are currently planted
- What stage of the growing season we're in
- What varieties are being grown

Also reference @durham-historical-weather.md to compare today's weather to typical conditions for this date.

## Step 3: Ensure Diary Directory Exists

Create the diary directory if it doesn't exist: !`mkdir -p diary`

## Step 4: Check for Existing Entry

Check if diary/YYYY-MM-DD.md already exists (where YYYY-MM-DD is today's date).
- If it exists, read it and inform the user you'll be appending to today's entry
- If not, inform the user you're creating a new entry

## Step 5: Interactive Questions

Based on the garden strategy context, ask the user the following questions interactively:

1. **Crops Observed Today**: Which crops did you check on or harvest from today? (Suggest crops from the strategy file)

2. **Crop Observations**: For each crop mentioned, ask for specific observations:
   - Growth stage, health status
   - Any flowering, fruiting, or harvest amounts
   - Any notable changes since last observation

3. **Tasks Completed**: What garden work did you do today?
   - Planting, transplanting
   - Watering, fertilizing
   - Pest management, disease treatment
   - Harvesting
   - Weeding, mulching
   - Other maintenance

4. **Problems & Issues**: Did you observe any problems today?
   - Diseases (specify which, which crops)
   - Pests (specify which, which crops)
   - Heat stress, water stress
   - Nutrient deficiencies
   - Any crop failures or struggles

5. **Successes & Harvests**: Any positive observations?
   - Good harvests (what, how much)
   - Varieties performing exceptionally well
   - Techniques or strategies working well
   - Any pleasant surprises

6. **Plans & Next Steps**: What needs doing soon?
   - Upcoming plantings or transplants
   - Materials or supplies to buy
   - Maintenance tasks scheduled
   - Experiments to try

## Step 6: Format and Write Entry

Create a markdown entry with this structure:

```markdown
# Garden Diary - [Full Date]

## Weather (Auto-fetched)
- **Temperature**: [Current temp]°F
- **Heat Index**: [Heat index]°F
- **Humidity**: [Humidity]%
- **Conditions**: [Current conditions]
- **Context**: [Compare to historical norms - is this typical? Unseasonably hot/cold? Heat index above/below normal?]

## Crops Observed
[Format user's observations by crop as a bulleted list or subsections]

## Tasks Completed
- [User inputs as bullet points]

## Problems & Issues
[User inputs, or "None observed" if none reported]

## Successes & Harvests
[User inputs, or "None to report" if none]

## Plans & Next Steps
- [User inputs as bullet points]

---
*Weather data fetched from Weather.gov/Weather Underground for Durham, NC 27707*
*Entry created: [timestamp]*
```

## Step 7: Write to File

If this is a new entry:
- Write the complete entry to diary/YYYY-MM-DD.md

If appending to existing entry:
- Add a separator (like `---` or timestamp header)
- Append the new observations below existing content

Confirm to the user that the entry has been created/updated at diary/YYYY-MM-DD.md
