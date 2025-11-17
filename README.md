# Durham NC Food Garden Planning

A comprehensive planning system for a food garden in Durham, North Carolina (27707, USDA Zone 7b/8a), built with [Claude Code](https://claude.com/claude-code).

## Overview

This repository contains detailed planning, historical weather data, and AI-powered advisors for managing a productive food garden in Durham's specific climate conditions.

**Garden Type**: Raised beds + containers
**Focus**: High-volume production, climate adaptation, budget-friendly practices
**Cuisines**: Asian, Mexican, Italian

## Repository Contents

### Planning Documents

- **[garden-setup.md](garden-setup.md)** - Complete garden infrastructure details
  - 3 raised beds (~79 sq ft total)
  - 10-20 containers (1 cu ft each)
  - Resources: 9 chickens, composting system, irrigation plans
  - Past successes and challenges from 2025

- **[2026-garden-strategy.md](2026-garden-strategy.md)** - Comprehensive growing plan
  - Month-by-month planting calendar (Feb-Nov 2026)
  - 20+ heat-tolerant varieties for Durham climate
  - Succession planting schedules
  - Bed layouts and companion planting
  - Disease prevention strategies
  - Expected yields: 600-900 lbs tomatoes, 400-800 cucumbers, etc.

- **[2026-shopping-list.md](2026-shopping-list.md)** - Complete supply list
  - Seeds from Southern Exposure, Baker Creek, Johnny's
  - Irrigation supplies (WiFi smart timer, soaker hoses)
  - Soil amendments (bulk compost delivery)
  - Local Durham suppliers (Lowe's, Barnes Supply, Triangle Mulch)
  - Budget: ~$500-600

### Climate Data

- **[durham-historical-weather.md](durham-historical-weather.md)** - Historical weather reference
  - 30-year climate normals (1991-2020) baseline
  - Recent detailed data (2020-2025)
  - Climate change trend analysis
    - Growing season +8 days longer
    - +20% more 90°F+ days
    - +50% increase in heavy rain events
  - Extreme weather events documented
  - Food gardening implications

### AI Assistants

Four specialized Claude Code agents in `.claude/agents/`:

1. **durham-garden-advisor** - Master gardener expertise
   - Plant selection and varieties for Durham
   - Planting schedules and techniques
   - Pest management and soil amendments
   - Budget-friendly solutions

2. **durham-climate-advisor** - Weather and climate analysis
   - Historical weather data interpretation
   - Frost date trends and analysis
   - Heat wave and precipitation patterns
   - Climate-informed planting recommendations

3. **garden-strategy-planner** - Strategic planning
   - Interactive garden planning sessions
   - Crop selection and quantities
   - Season-by-season strategies
   - Learning from past experiences

4. **weather-strategy-updater** - Strategy updates
   - Updates garden strategy based on weather patterns
   - Adapts plans to climate conditions

### Garden Diary System

**NEW: Video-based diary entries!** Record garden tours on your phone and AI automatically generates detailed diary entries.

**Commands in `.claude/commands/`:**

- `/diary` - Full interactive diary entry (original system)
- `/quick-note` - Fast note appended to today's entry
- `/process-diary` - **Process video tours into diary entries**
  - Transcribes your narration
  - Analyzes plants, health, problems visually
  - Reads plant tags and labels
  - Tracks growth over time
  - Fetches weather data
  - Generates structured markdown entry

**Workflow:**
1. Record 1-5 min video tour of garden on phone (narrate what you see)
2. Upload to `diary-inbox/YYYY-MM-DD/` folder
3. Run `/process-diary` in Claude Code
4. Review generated entry in `diary/YYYY-MM-DD.md`

See **[MOBILE-DIARY-GUIDE.md](MOBILE-DIARY-GUIDE.md)** for complete mobile workflow.
See **[AUTOMATION-SETUP.md](AUTOMATION-SETUP.md)** for GitHub Actions automation.

### Configuration

- **[CLAUDE.md](CLAUDE.md)** - Repository guidance for Claude Code
  - Project context and priorities
  - Climate factors and constraints
  - Agent descriptions and usage

## Quick Start

### For 2026 Growing Season

1. **November-December 2025**
   - Start composting chicken manure
   - Order seeds from shopping list
   - Schedule compost delivery for mid-March

2. **Late February 2026**
   - Start peppers, tomatillos, tomatoes indoors
   - Begin succession seed starting

3. **Mid-March 2026**
   - Receive bulk compost delivery
   - Amend all beds with 2-3" compost
   - Install soaker hose system

4. **Mid-April 2026**
   - Major transplant week (after last frost ~April 10)
   - Follow detailed calendar in 2026-garden-strategy.md

## Key Features

### Climate-Adapted Planning
- Heat-tolerant varieties for Durham's hot summers
- Frost-aware planting schedules
- Irrigation planning for summer dry spells

### Data-Driven Decisions
- Historical weather patterns inform planting timing
- Climate change trends guide variety selection
- Past performance tracked for continuous improvement

### Budget-Conscious
- Free resources: pine straw mulch, chicken manure
- Bulk purchasing strategies
- Seed starting vs. transplant cost analysis

### High-Volume Production
- Succession plantings for continuous harvest
- Expected peak: 100+ lbs produce/week in July
- Designed for household use + neighbor sharing

## Climate Context

**Durham Hardening Zone**: 7b/8a

**Recent Trends (2020-2025 vs 1991-2020)**:
- Last spring frost: April 10 (was April 15) - 5 days earlier
- First fall frost: November 12 (was November 10) - 2 days later
- Growing season: 217 days (was 209 days) - 8 days longer
- **Humid heat stress**: Heat index >100°F for ~15 days in July (20-25 days in hot years)
  - Durham's 70-80% humidity prevents plant transpiration cooling
  - Pollination fails at heat index 100-105°F even when air temp is only 90-95°F
- Precipitation: Similar totals but more intense events, longer dry spells

**Implication**: Climate change is extending the growing season but **humid heat stress** is Durham's critical challenge - must use Southern humid-heat-tolerant varieties, not California "heat-tolerant" varieties.

## 2025 Lessons Learned

**Successes**:
- Peppers (purple bell, banana, jalapeño, poblano) - excellent
- Herbs (basil, cilantro, parsley, thai basil, etc.) - thrived
- Tomatillos - performed well
- Marigolds - excellent companion plants

**Challenges**:
- Late start (late May vs mid-April) caused issues
- Cucurbits (melons, squash, cucumbers) failed - **humid heat stress**, disease, late planting
- **Root cause**: Planted when heat index already >100°F; likely used California-bred varieties that fail in Durham's humidity

**2026 Improvements**:
- Start 6 weeks earlier (mid-April transplants) for fruit set before July's humid heat
- **Humid-heat-tolerant varieties** bred for Southern humidity:
  - Arkansas Traveler tomatoes (bred for Arkansas humid heat)
  - Poinsett 76 cucumbers (bred for hot, humid Southeast)
  - Costata Romanesco squash (Italian, bred for Mediterranean humidity)
- Succession plantings for backup during humid heat stress periods
- Soaker hose irrigation system
- Proactive disease prevention (humidity amplifies fungal diseases)
- Accept 3-4 week production gap mid-July to early-August (heat index >100°F)

## Using This Repository

### With Claude Code

This repository is designed to work with [Claude Code](https://claude.com/claude-code). The specialized agents can:
- Answer Durham-specific gardening questions
- Analyze weather patterns for planning
- Help create and update garden strategies
- Provide variety recommendations
- Troubleshoot problems

### Without Claude Code

All planning documents are markdown files that can be:
- Read in any text editor or markdown viewer
- Printed for reference
- Updated as you track progress
- Shared with other gardeners

## Contributing

This is a personal garden planning repository, but if you're also gardening in Durham NC (or similar climate), feel free to fork and adapt for your needs.

## License

This documentation is shared freely. Use and adapt as needed for your own garden planning.

---

**Last Updated**: November 2025
**Location**: Durham, NC 27707
**Zone**: USDA 7b/8a
