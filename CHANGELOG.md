# Changelog

## [3.0.0] - 2026-02-24

### Changed - MAJOR UPDATE
- **Corrected monitor input configuration** for Samsung ViewFinity S65UC (each monitor has 1 HDMI, 1 DP, 1 USB-C)
- Personal Mac now uses HDMI inputs on both monitors (simplest setup)
- Work Mac now uses DisplayPort inputs via BENFEI adapters
- HP Dock now uses USB-C inputs via DP→HDMI→USB-C conversion
- Better Display hotkeys updated: Cmd+1=HDMI, Cmd+2=DP, Cmd+3=USB-C

### Added
- HDMI to USB-C adapter equipment card
- Detailed signal chains showing adapter requirements per computer
- USB power warnings for BENFEI adapters
- Notes about two-stage conversion for HP Dock

### Updated
- All connection diagrams and signal chains
- Equipment shopping list with accurate counts
- Wizard data for all 3 computers (6 hardware steps)
- Software configuration instructions
- Final summary tables

### Breaking Changes
- Previous guide showed incorrect input usage (multiple computers on same input type)
- Equipment requirements changed (added HDMI→USB-C adapters, adjusted BENFEI count)

## [2.0.0] - 2026-02-24

### Changed
- Updated from 3-monitor setup to 2-monitor setup
- New monitors: 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- Simplified connections using native DisplayPort where possible
- Software updates: Lunar → Better Display, Barrier → InputLeap
- Updated all guide sections and wizard steps

### Added
- DisplayPort to HDMI adapter for HP Dock connections
- Better input management using Better Display DDC/CI

### Removed
- CENTER monitor references (all 1B, 2B, 3B sections)
- HDMI switch equipment (no longer needed)
- Barrier software references (replaced with InputLeap)
- Lunar software references (replaced with Better Display)

### Updated
- Total wizard steps: 13 → 9
- Equipment quantities for 2-monitor setup
- Software configuration instructions
- Quick reference tables (LEFT and RIGHT only)
- Connection diagrams and signal chains
- Monitor input switching via Better Display
