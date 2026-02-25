# KVM Setup Guide

Complete visual guide for connecting 3 computers to 2 monitors with KVM functionality.

## Current Setup
- **Monitors:** 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- **Computers:** Personal Mac, Work Mac, HP Dock
- **Features:** DDC/CI switching via Better Display, InputLeap for unified mouse/keyboard

## Monitor Inputs
Each Samsung ViewFinity S65UC has:
- 1x HDMI 2.0 input
- 1x DisplayPort 1.2 input
- 1x USB-C input (with DisplayPort Alt Mode, 90W power delivery)

## Connection Strategy
- All 3 computers connect to both monitors using different input types
- Better Display switches monitor inputs via DDC/CI commands
- Hotkeys (Cmd+1/2/3) switch all monitors simultaneously

## Deployment
- Live site: https://vercel-kvm.vercel.app/
- Deployed via Vercel
- Updates: Push to main branch or `vercel --prod`

## Development
- Single-file HTML application
- No build process required
- Edit `index.html` and copy to `public/` for deployment

## Version
Current version: 2.0.0 (2-monitor setup)
