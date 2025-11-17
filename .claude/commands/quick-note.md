---
description: Quickly add a brief observation to today's garden diary
allowed-tools: Write, Read, Bash(date:*)
model: haiku
---

# Quick Garden Note

Add a fast observation to today's diary entry. Perfect for brief notes while you're in the garden!

## Step 1: Get Today's Date

Get today's date: !`date +%Y-%m-%d`

## Step 2: Get Quick Observation

Ask the user just one simple question:

**"What did you observe or do in the garden?"**

Keep it casual and brief. Examples you can show:
- "Harvested 3 tomatoes, 1 was split from rain"
- "Basil is bolting, needs to be cut back"
- "Watered everything, very dry today"
- "Spotted aphids on pepper plants"

## Step 3: Check for Today's Entry

Check if diary/YYYY-MM-DD.md exists (where YYYY-MM-DD is today's date).

## Step 4: Add the Note

**If the diary entry exists:**
- Read the existing entry
- Find the "## Quick Notes" section if it exists
- If "Quick Notes" section doesn't exist, add it at the end before the footer
- Append the note with a timestamp: `- [HH:MM] User's observation`

**If no diary entry exists yet:**
- Create a simple entry with:
```markdown
# Garden Diary - [Full Date]

## Quick Notes
- [HH:MM] User's observation

---
*Quick note added: [timestamp]*
```

## Step 5: Confirm

Tell the user: "Note added to diary/YYYY-MM-DD.md! Use `/diary` later for a detailed entry."

## Tips for Users

Quick notes are perfect for:
- Fast observations while in the garden
- Things you notice but don't have time to document fully
- Reminders of what to investigate later
- Harvest tracking

You can add multiple quick notes throughout the day, then use `/diary` in the evening to add full details!
