# Changelog

## [3.0.0] - 2026-02-24

### Changed
- **DDC/CI Fix:** Direct USB-C to HDMI connections for MacBooks (bypassing UGREEN hub)
- **HP Dock Upgrade:** Replaced VGA with DisplayPort to HDMI conversion
- **UGREEN Hubs:** Repurposed for Ethernet only (not used for video)
- All connections now use consistent HDMI → EDID → BENFEI → DP chain

### Added
- Comprehensive shopping list with "Have" vs "Need to Buy" sections
- DP to HDMI adapter equipment cards
- DDC/CI explanation in software setup section
- Ethernet connection notes for MacBooks

### Updated
- Equipment quantities for v3.0.0 inventory
- All connection diagrams and signal chains
- JavaScript wizard data for all three computers
- Software configuration documentation

**Why this update?** The UGREEN hubs don't pass DDC/CI commands needed for Lunar to automatically switch monitor inputs. Direct connections solve this issue.

## [2.0.0] - 2026-02-24

### Changed
- Updated from 3-monitor setup to 2-monitor setup
- New monitors: 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- Simplified connections using native DisplayPort
- Removed HDMI switch (no longer needed)
- Updated all guide sections and wizard steps

### Removed
- CENTER monitor references (all 1B, 2B, 3B sections)
- HDMI switch equipment
- Reduced BENFEI adapter requirements

### Updated
- Total wizard steps: 13 → 9
- Equipment quantities
- Software configuration for 2 monitors
- Quick reference tables
