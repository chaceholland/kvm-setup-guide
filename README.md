# KVM Setup Guide

Complete visual guide for connecting 3 computers to 2 monitors with KVM functionality.

## Current Setup
- **Monitors:** 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- **Computers:** Personal Mac, Work Mac, HP Dock
- **Features:** DDC/CI switching via Better Display, InputLeap for unified mouse/keyboard

## Monitor Inputs (IMPORTANT)

Each Samsung ViewFinity S65UC 34" has exactly:
- **1x HDMI 2.0 input**
- **1x DisplayPort 1.2 input**
- **1x USB-C input** (with DisplayPort Alt Mode, 90W power delivery)

## Connection Strategy

**Input Assignment:**
- Personal Mac → Both monitors via **HDMI** (simplest, direct after EDID)
- Work Mac → Both monitors via **DisplayPort** (USB-C→HDMI→EDID→Coupler→BENFEI→DP)
- HP Dock → Both monitors via **USB-C** (DP→HDMI→EDID→Coupler→HDMI-to-USB-C)

**Better Display Hotkeys:**
- Cmd+1: Switch both monitors to HDMI (Personal Mac)
- Cmd+2: Switch both monitors to DisplayPort (Work Mac)
- Cmd+3: Switch both monitors to USB-C (HP Dock)

## Deployment
- Live site: https://vercel-kvm.vercel.app/
- Deployed via Vercel
- Updates: Push to main branch or `vercel --prod`

## Development
- Single-file HTML application
- No build process required
- Edit `index.html` and copy to `public/` for deployment

## Version
Current version: 3.0.0 (corrected monitor inputs)
