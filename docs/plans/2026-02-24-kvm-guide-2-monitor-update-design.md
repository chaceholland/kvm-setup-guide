# KVM Guide Update: 3 Monitors → 2 Monitors Design

**Date:** 2026-02-24
**Author:** Claude Code
**Status:** Approved

## Overview

Update the KVM Setup Guide (https://vercel-kvm.vercel.app/) to reflect a hardware change from 3 monitors to 2 monitors. The new monitors are 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO).

## Requirements

- Replace 3-monitor setup (LEFT, CENTER, RIGHT) with 2-monitor setup (LEFT, RIGHT)
- All 3 computers (Personal Mac, Work Mac, HP Dock) connect to both monitors
- Simplify connections using native DisplayPort where possible
- Update both the full guide and interactive wizard
- Maintain all existing functionality (Lunar, Barrier, hotkeys)

## Approach: Simplified with DisplayPort

We're using **Approach B** which simplifies the setup by leveraging native DisplayPort connections instead of HDMI→DP adapters.

### Key Benefits
- Fewer adapters = fewer points of failure
- Better signal quality with direct DP connections
- Cleaner cable management
- Reduced equipment cost

## Architecture Changes

### Monitor Configuration

**Previous Setup:**
- 3 monitors (LEFT, CENTER, RIGHT)
- Mix of HDMI and DisplayPort connections
- HDMI switch for CENTER monitor sharing

**New Setup:**
- 2x Samsung ViewFinity S65UC 34" monitors (LEFT, RIGHT)
- Monitor specs:
  - HDMI 2.0 inputs
  - DisplayPort 1.2 inputs
  - USB-C with video/data/90W power
  - Built-in USB hub and Ethernet
- Direct DisplayPort connections preferred
- No HDMI switch needed

### Computer Connections

**Personal MacBook:**
- LEFT Monitor: MacBook USB-C → UGREEN Hub → HDMI → EDID → DP adapter → Monitor DP
- RIGHT Monitor: MacBook USB-C → USB-C to DP cable → EDID → Monitor DP

**Work MacBook:**
- LEFT Monitor: Same pattern as Personal Mac (using second UGREEN Hub)
- RIGHT Monitor: Same pattern as Personal Mac

**HP Dock:**
- LEFT Monitor: HP Dock → DP/VGA → Monitor
- RIGHT Monitor: HP Dock → DP/VGA → Monitor

## Equipment Changes

### Remove/Reduce
- ❌ HDMI switch (no longer needed without CENTER monitor)
- ⬇️ BENFEI HDMI→DP adapters (from 4 to 0-2, depending on final connection strategy)
- ⬇️ HDMI couplers (fewer adapters = fewer couplers)

### Add
- ➕ 4-6x USB-C to DisplayPort cables
- 🔄 May reuse existing USB-C to HDMI cables for some connections

### Keep
- ✅ 2x UGREEN Revodok Pro hubs
- ✅ EDID emulators (use 2x 1440p or existing mix)
- ✅ VGA adapters (if HP Dock requires them)

## Software Configuration

### Lunar DDC/CI Updates
- **Cmd+1**: Switch both monitors to Personal Mac
- **Cmd+2**: Switch both monitors to Work Mac
- **Cmd+3**: Switch both monitors to HP Dock
- Remove all CENTER monitor input configurations
- Update monitor detection to expect 2 monitors

### Barrier
- No changes needed (works the same with 2 monitors)

### Quick Reference Tables
- Change from 3-column (LEFT/CENTER/RIGHT) to 2-column (LEFT/RIGHT)
- Update connection summaries
- Remove HDMI switch references

## Guide Structure Updates

### Page Header
- Change: "Connecting 3 Computers to 3 Monitors" → "Connecting 3 Computers to 2 Monitors"

### Table of Contents
- Part 0: Equipment Overview (update monitor specs)
- Part 1: Personal MacBook → "Connect to LEFT and RIGHT monitors"
- Part 2: Work MacBook → "Connect to LEFT and RIGHT monitors"
- Part 3: HP Dock → "Connect to LEFT and RIGHT monitors"

### Connection Sections
- Remove all "B" sections (CENTER monitor connections: 1B, 2B, 3B)
- Relabel remaining sections:
  - 1A (LEFT) and 1C (RIGHT) → 1A and 1B
  - 2A (LEFT) and 2C (RIGHT) → 2A and 2B
  - 3A (LEFT) and 3C (RIGHT) → 3A and 3B

### Interactive Wizard
- Update step count from 13 to approximately 9-10 steps
- Remove CENTER monitor steps from wizardData object
- Update progress tracking (e.g., "2/2 complete" instead of "3/3 complete")
- Update completion celebration screen
- Update computer tab badges to show correct progress

### Visual Elements
- Update equipment cards with ViewFinity S65UC specifications
- Update all signal chain diagrams to show only LEFT/RIGHT paths
- Remove CENTER monitor references from inline photos
- Update final summary tables

## Data Flow

### Static Content Updates (HTML)
1. Header and subtitle text
2. Table of contents descriptions
3. Equipment overview section
4. Connection guide sections (remove 1B, 2B, 3B)
5. Final summary tables
6. All "3 monitors" text → "2 monitors"

### Dynamic Content Updates (JavaScript)
1. `wizardData` object - remove CENTER monitor steps
2. Progress calculation (total steps reduced)
3. Computer section completion tracking
4. Final celebration step count
5. Quick reference tables in completion screen

## Testing Considerations

After implementation, verify:
- All monitor references show "2 monitors" or "both monitors"
- No broken "CENTER" references remain
- Signal chain diagrams render correctly with 2 monitors
- Wizard progress tracking calculates correctly
- Equipment quantities are accurate
- All hyperlinks to equipment still work
- Print layout still works properly

## Migration Notes

This is a documentation-only update. No actual hardware migration steps are needed in the guide itself, but users following the guide will:
- Purchase 2 monitors instead of 3
- Need fewer adapters
- Have simpler setup process
- Experience faster completion time

## Success Criteria

✅ All references to 3 monitors updated to 2 monitors
✅ CENTER monitor sections completely removed
✅ Equipment list reflects new monitor model and reduced accessories
✅ Connection diagrams show only LEFT and RIGHT paths
✅ Interactive wizard step count and progress accurate
✅ Software configuration instructions updated
✅ Guide deploys successfully to Vercel
✅ Both Full Guide and Interactive Wizard tabs work correctly
