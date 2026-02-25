# KVM Setup Guide

Complete visual guide for connecting 3 computers to 2 monitors with KVM functionality.

## Current Setup (v3.0.0)
- **Monitors:** 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- **Computers:** Personal Mac, Work Mac, HP Dock
- **Features:** DDC/CI switching via Lunar (direct connections), Barrier for unified mouse/keyboard
- **Connection Method:** Direct USB-C/DP to HDMI for DDC/CI compatibility

## Recent Updates
- **v3.0.0:** Fixed DDC/CI issues by using direct connections instead of hubs for video
- **v2.0.0:** Migration to 2 Samsung ViewFinity monitors

## Deployment
- Live site: https://vercel-kvm.vercel.app/
- Deployed via Vercel
- Updates: Push to main branch or `vercel --prod`

## Development
- Single-file HTML application
- No build process required
- Edit `index.html` and copy to `public/` for deployment
