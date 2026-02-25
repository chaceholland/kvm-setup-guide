# DDC/CI Fix & Shopping List Design

**Date:** 2026-02-24
**Status:** Approved
**Version:** 3.0.0 (Post 2-monitor migration)

## Problem Statement

The UGREEN Revodok Pro 6-in-1 Hub does not pass DDC/CI commands through its HDMI output. This prevents Lunar from switching monitor inputs, breaking the KVM functionality for automated monitor switching.

## Solution Overview

Use direct USB-C to HDMI connections for MacBooks (bypassing the hub for video), and convert HP Dock's DisplayPort to HDMI to maintain a consistent equipment chain across all computers. UGREEN hubs will be repurposed for Ethernet only.

## Architecture

### Personal MacBook
- **USB-C port 1:** Direct to LEFT monitor
  `MacBook USB-C → USB-C to HDMI cable → EDID 1440p → Coupler → BENFEI → DP cable → LEFT Monitor`

- **USB-C port 2:** Direct to RIGHT monitor
  `MacBook USB-C → USB-C to HDMI cable → EDID 1440p → Coupler → BENFEI → DP cable → RIGHT Monitor`

- **USB-C port 3:** UGREEN Hub (Ethernet only, no video)

### Work MacBook
- Identical configuration to Personal MacBook
- Uses second UGREEN Hub for Ethernet

### HP Dock
- **DP port 1:** To LEFT monitor
  `HP Dock DP → DP to HDMI adapter → HDMI cable → EDID 1440p → Coupler → BENFEI → DP cable → LEFT Monitor`

- **DP port 2:** To RIGHT monitor
  `HP Dock DP → DP to HDMI adapter → HDMI cable → EDID 1440p → Coupler → BENFEI → DP cable → RIGHT Monitor`

### Key Changes from v2.0.0
- ❌ **Remove:** UGREEN Hub from video path for MacBooks (was: `USB-C → Hub → HDMI → Monitor`)
- ✅ **Add:** Direct USB-C to HDMI cables for MacBook LEFT monitors
- ✅ **Add:** DP to HDMI adapters for HP Dock (replacing VGA cables)
- ✅ **Upgrade:** All connections now use consistent HDMI → EDID → BENFEI → DP chain
- ✅ **Keep:** UGREEN Hubs repurposed for Ethernet only

## Equipment Inventory

### Current Inventory (Have)
- 2× Samsung ViewFinity S65UC 34" monitors
- 2× UGREEN Revodok Pro 6-in-1 Hub
- 4× BENFEI HDMI→DP adapters (with USB power)
- 2× EDID 1440p emulators
- 4× EDID 1080p emulators
- 4× HDMI couplers
- 2× USB-C to HDMI cables
- ~4+ DisplayPort cables

### New Equipment to Purchase
- **2× USB-C to HDMI cables** - For MacBook LEFT monitors
- **4× EDID 1440p emulators** - Replace existing mixed inventory for consistency
- **2× BENFEI HDMI→DP adapters** - For HP Dock connections
- **2× DP to HDMI adapters** - Convert HP Dock DP output to HDMI
- **2× HDMI couplers** - For HP Dock chain
- **4-6× Standard HDMI cables** - Various connections between equipment

**Estimated Cost:** $250-350

### Total Inventory After Purchase
- 4× USB-C to HDMI cables (2 per MacBook)
- 6× EDID 1440p emulators (4 MacBooks + 2 HP)
- 6× BENFEI HDMI→DP adapters (4 MacBooks + 2 HP)
- 6× HDMI couplers (4 MacBooks + 2 HP)
- 2× DP to HDMI adapters (HP Dock only)
- 10-12× HDMI cables
- 6× DisplayPort cables (BENFEI to monitors)

## Guide Updates

### Files to Modify
1. `index.html` - Main KVM guide
2. `public/index.html` - Deployment copy

### Update Sections

#### Part 0: Equipment Overview
- Update UGREEN Hub card description to note "Ethernet only (DDC/CI not supported for video)"
- Add new equipment card for DP to HDMI adapters
- Update all quantity labels to reflect new inventory
- Add shopping list section with "Have" vs "Need to Buy" tables

#### Part 1: Personal MacBook Setup
- **Connection 1A (LEFT):**
  - Remove UGREEN Hub from signal chain
  - Update to: `MacBook USB-C → USB-C to HDMI → EDID 1440p → Coupler → BENFEI → DP → Monitor`
  - Remove hub equipment photo, remove hub USB power note
  - Update warning box to reference BENFEI power from USB power adapter

- **Connection 1B (RIGHT):**
  - No changes (already direct USB-C to HDMI)

- Add section note: "UGREEN Hub plugged into USB-C port 3 for Ethernet"

#### Part 2: Work MacBook Setup
- Identical changes to Part 1

#### Part 3: HP Dock Setup
- **Connection 3A (LEFT):**
  - Replace VGA chain with: `HP Dock DP → DP to HDMI adapter → HDMI → EDID 1440p → Coupler → BENFEI → DP → Monitor`
  - Update equipment photos
  - Update signal chain diagram

- **Connection 3B (RIGHT):**
  - Same changes as 3A

#### JavaScript Wizard Data
- Update `wizardData.personal.steps[0]` (1A) - remove hub from equipment array and signal chain
- Update `wizardData.work.steps[0]` (2A) - remove hub from equipment array and signal chain
- Update `wizardData.hp.steps[0]` (3A) - replace VGA with DP→HDMI→EDID→BENFEI→DP chain
- Update `wizardData.hp.steps[1]` (3B) - same as 3A
- Update all detailed steps to reflect new connections

#### Software Setup Section
- Add explanation of DDC/CI requirement
- Note that direct connections are necessary for Lunar to work
- Mention UGREEN hubs are for Ethernet only

## Benefits

1. **DDC/CI Works:** Lunar can now switch monitor inputs automatically
2. **Better Quality:** HP Dock uses DP instead of VGA
3. **Consistent Setup:** All computers use same equipment chain (HDMI → EDID → BENFEI → DP)
4. **Ethernet Preserved:** UGREEN hubs still provide wired network for MacBooks
5. **Future-Proof:** Direct connections are more reliable for macOS display management

## Risks & Mitigations

**Risk:** More cables and adapters increase complexity
**Mitigation:** Guide clearly documents each connection with photos and signal chains

**Risk:** USB-C ports all occupied on MacBooks
**Mitigation:** MacBooks have 3 USB-C ports (2 monitors + 1 hub), plus unused HDMI port for future expansion

**Risk:** BENFEI adapters require USB power
**Mitigation:** Guide emphasizes this in warning boxes, can power from USB wall adapters

## Testing Plan

1. Connect one MacBook following new guide
2. Test DDC/CI with Lunar (Cmd+1/2/3 should switch monitors)
3. Verify Ethernet works through UGREEN hub
4. Complete setup for all three computers
5. Test full KVM switching workflow
6. Verify no window rearrangement when switching

## Success Criteria

- ✅ Lunar successfully switches both monitors via DDC/CI
- ✅ No window rearrangement when switching between computers
- ✅ Ethernet works on both MacBooks
- ✅ All equipment properly documented in guide
- ✅ Shopping list accurate and complete
- ✅ Guide deployed to Vercel

## Version History

- **v1.0.0** - Original 3-monitor setup with HDMI switch
- **v2.0.0** - Migration to 2 Samsung ViewFinity monitors
- **v3.0.0** - DDC/CI fix with direct connections (this design)
