# KVM Guide Corrected Monitor Inputs Design

**Date:** 2026-02-24
**Author:** Claude Code
**Status:** Approved

## Problem Statement

The current guide incorrectly assumes each Samsung ViewFinity S65UC monitor has multiple DisplayPort inputs. In reality, each monitor has:
- **1 HDMI input**
- **1 DisplayPort input**
- **1 USB-C input**

This requires redesigning all connections to ensure each computer uses a DIFFERENT input type on each monitor.

## Requirements

- 3 computers (Personal Mac, Work Mac, HP Dock) → 2 monitors
- Each computer connects to both monitors
- EDID emulators must be inline in every connection (HDMI IN/OUT)
- Better Display switches both monitors simultaneously via DDC/CI
- Each computer uses the same input type on both monitors

## Approved Approach

**Input Assignment:**
- **Personal Mac** → Both monitors via **HDMI** (simplest)
- **Work Mac** → Both monitors via **DisplayPort** (1 adapter per monitor)
- **HP Dock** → Both monitors via **USB-C** (2 adapters per monitor)

**Better Display Hotkeys:**
- Cmd+1: Switch both monitors to HDMI (Personal Mac)
- Cmd+2: Switch both monitors to DisplayPort (Work Mac)
- Cmd+3: Switch both monitors to USB-C (HP Dock)

## Architecture

### Overall System

```
Monitor 1 (LEFT)          Monitor 2 (RIGHT)
├─ HDMI    → Personal     ├─ HDMI    → Personal
├─ DP      → Work         ├─ DP      → Work  
└─ USB-C   → HP Dock      └─ USB-C   → HP Dock
```

### Signal Flow Pattern (Every Connection)

```
Computer Output
    ↓
(Adapter to HDMI if needed)
    ↓
EDID Emulator 1440p (HDMI IN/OUT)
    ↓
(HDMI Coupler if adapter follows)
    ↓
(HDMI-to-Monitor-Input adapter if needed)
    ↓
Monitor Input
```

**Key Constraint:** EDID emulators require HDMI, so all signals convert to HDMI before EDID, then convert to final input type after EDID.

## Equipment Requirements

### Monitors
- 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)

### EDID Emulators
- 6x EDID 1440p emulators (one per connection)
- Male HDMI IN/OUT

### Adapters & Cables
- **4x** USB-C to HDMI cables (2 per MacBook)
- **2x** DP to HDMI adapters (HP Dock DP outputs)
- **4x** BENFEI HDMI→DP adapters with USB power (Work Mac)
- **2x** HDMI to USB-C adapters (HP Dock to monitors)
- **6x** HDMI couplers (female-female)
- **2x** UGREEN hubs (Ethernet only, NOT for video)

### Software
- Better Display (DDC/CI input switching)
- InputLeap (keyboard/mouse sharing)

### Equipment Count Per Computer

**Personal Mac:**
- 2 USB-C to HDMI cables
- 2 EDID emulators

**Work Mac:**
- 2 USB-C to HDMI cables
- 2 EDID emulators
- 4 HDMI couplers
- 2 BENFEI HDMI→DP adapters (with USB power)

**HP Dock:**
- 2 DP to HDMI adapters
- 2 EDID emulators
- 4 HDMI couplers
- 2 HDMI to USB-C adapters

## Connection Details

### Personal Mac → Both Monitors (HDMI)

**LEFT Monitor:**
```
MacBook USB-C → USB-C to HDMI cable → EDID 1440p → Monitor 1 HDMI
```

**RIGHT Monitor:**
```
MacBook USB-C → USB-C to HDMI cable → EDID 1440p → Monitor 2 HDMI
```

**Notes:** 
- Simplest setup (no couplers or extra adapters)
- EDID male output connects directly to monitor HDMI female input

---

### Work Mac → Both Monitors (DisplayPort)

**LEFT Monitor:**
```
MacBook USB-C 
    → USB-C to HDMI cable 
    → EDID 1440p (male OUT)
    → HDMI Coupler (female-female)
    → BENFEI HDMI→DP adapter (male IN, DP OUT)
    → Monitor 1 DisplayPort
```

**RIGHT Monitor:**
```
MacBook USB-C 
    → USB-C to HDMI cable 
    → EDID 1440p (male OUT)
    → HDMI Coupler (female-female)
    → BENFEI HDMI→DP adapter (male IN, DP OUT)
    → Monitor 2 DisplayPort
```

**Notes:**
- BENFEI requires USB power (wall adapter or USB port)
- Coupler needed to connect EDID male OUT to BENFEI male IN

---

### HP Dock → Both Monitors (USB-C)

**LEFT Monitor:**
```
HP Dock DP output
    → DP to HDMI adapter
    → (HDMI cable if needed for distance)
    → EDID 1440p (male OUT)
    → HDMI Coupler (female-female)
    → HDMI to USB-C adapter
    → Monitor 1 USB-C
```

**RIGHT Monitor:**
```
HP Dock DP output
    → DP to HDMI adapter
    → (HDMI cable if needed)
    → EDID 1440p (male OUT)
    → HDMI Coupler (female-female)
    → HDMI to USB-C adapter
    → Monitor 2 USB-C
```

**Notes:**
- Two conversion stages: DP→HDMI, then HDMI→USB-C
- Most complex chain but uses HP's native DP outputs

---

### UGREEN Hub Usage

**Purpose:** Ethernet connection for MacBooks (InputLeap networking)

**NOT used for video** because:
- Hubs block DDC/CI commands
- Better Display can't switch inputs through hubs
- Direct USB-C to HDMI connection required for DDC/CI

## Software Configuration

### Better Display Setup

1. Install Better Display on Personal Mac (or primary computer)
2. Grant permissions:
   - Accessibility (required for DDC/CI)
   - Screen Recording (for some features)
3. Verify both monitors appear in Better Display menu bar
4. Configure Input Source hotkeys:
   - **Cmd+1:** HDMI (Personal Mac)
   - **Cmd+2:** DisplayPort (Work Mac)
   - **Cmd+3:** USB-C (HP Dock)
5. Test: Press each hotkey, verify both monitors switch simultaneously

**Requirements:**
- Direct USB-C video connections (not through hubs)
- Monitors must support DDC/CI (ViewFinity does)

### InputLeap Setup

1. Install InputLeap on all 3 computers
2. Configure server/client:
   - Personal Mac: Server mode
   - Work Mac: Client mode
   - HP Laptop: Client mode
3. Arrange screens to match physical layout
4. Connect all computers to same network via Ethernet
5. Test mouse/keyboard sharing across computers

**Network:** Use UGREEN hubs for MacBook Ethernet

### EDID Emulator Function

**Automatic operation:**
- Stores monitor EDID (1440p resolution, capabilities)
- Computer always "sees" monitor as connected
- Prevents window rearrangement when switching inputs
- No configuration needed after physical connection

## Testing & Verification

### Hardware Checklist

- [ ] Personal Mac displays on both monitors (HDMI inputs)
- [ ] Work Mac displays on both monitors (DP inputs)
- [ ] HP Dock displays on both monitors (USB-C inputs)
- [ ] All BENFEI adapters have USB power
- [ ] All 6 EDID emulators inline in chains
- [ ] No signal degradation or artifacts

### Software Checklist

**Better Display:**
- [ ] Both monitors detected
- [ ] Cmd+1 switches both to HDMI
- [ ] Cmd+2 switches both to DP
- [ ] Cmd+3 switches both to USB-C
- [ ] Switches happen simultaneously
- [ ] No delay or flicker

**InputLeap:**
- [ ] Mouse moves between computers
- [ ] Keyboard works on all computers
- [ ] All computers reachable on network

**EDID:**
- [ ] Disconnect cable - windows stay in place
- [ ] Switch inputs - windows stay in place
- [ ] Reboot - windows restore correctly

## Troubleshooting

**Monitor not detected:**
- Check BENFEI USB power (if applicable)
- Verify EDID connected correctly
- Check all couplers seated properly

**Better Display can't switch:**
- Verify Accessibility permissions
- Ensure direct USB-C connection (not through hub)
- Confirm monitor supports DDC/CI

**InputLeap not working:**
- Check all computers on same network
- Verify firewall settings
- Confirm server IP address

## Migration from Current Guide

**Changes needed:**
1. Update all connection diagrams
2. Change Personal Mac from DP to HDMI connections
3. Update Work Mac to use DP (add BENFEI adapters)
4. Update HP Dock to use USB-C (add HDMI→USB-C adapters)
5. Update equipment lists and quantities
6. Update Better Display hotkey mappings
7. Update all wizard steps (6 hardware connections remain)

**Guide structure remains:**
- Part 0: Equipment Overview
- Part 1: Personal Mac (2 connections to LEFT/RIGHT)
- Part 2: Work Mac (2 connections to LEFT/RIGHT)
- Part 3: HP Dock (2 connections to LEFT/RIGHT)
- Part 4: Software Setup

## Success Criteria

✅ Each computer connects to both monitors
✅ Each computer uses unique input type on each monitor
✅ EDID inline in every connection
✅ Better Display switches both monitors simultaneously
✅ All connections properly documented and diagrammed
✅ Equipment list accurate
✅ Wizard reflects 6 total hardware connections + software
