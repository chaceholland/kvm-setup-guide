# DDC/CI Fix & Shopping List Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Update KVM guide to use direct USB-C connections for MacBooks and DP-to-HDMI adapters for HP Dock, fixing DDC/CI issues and adding comprehensive shopping list.

**Architecture:** Single-file HTML update targeting equipment section, connection diagrams (Personal/Work/HP), and JavaScript wizard data. Remove UGREEN Hub from video signal chains, update HP Dock from VGA to DP-HDMI-EDID-BENFEI chain, add shopping list with inventory tracking.

**Tech Stack:** Static HTML/CSS/JavaScript (no build process), deployed to Vercel

---

## Task 1: Update Equipment Overview - UGREEN Hub Description

**Files:**
- Modify: `index.html:284-290`

**Step 1: Update UGREEN Hub description**

Find the UGREEN Hub equipment card and update the description to note Ethernet-only use:

```html
<div class="description"><strong>What it does:</strong> Provides Ethernet and USB ports. <strong>⚠️ For Ethernet only:</strong> Does not pass DDC/CI commands through HDMI, so not used for video connections.</div>
```

**Step 2: Verify changes in browser**

Open `index.html` in browser and check equipment section shows updated UGREEN description

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: update UGREEN hub description for Ethernet-only use"
```

---

## Task 2: Add DP to HDMI Adapter Equipment Card

**Files:**
- Modify: `index.html:320` (after USB-C to HDMI card)

**Step 1: Add new equipment card**

Insert new card after the USB-C to HDMI cable card:

```html
                    <div class="equipment-card">
                        <div class="card-header" style="background: linear-gradient(135deg, #9c27b0 0%, #7b1fa2 100%);">🔌 DisplayPort to HDMI Adapter</div>
                        <div class="card-body">
                            <div class="photo-container"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" alt="DP to HDMI Adapter"></div>
                            <div class="port-labels"><span class="port-label dp">DP IN (Male)</span><span class="port-label hdmi">HDMI OUT (Female)</span></div>
                            <div class="description"><strong>What it does:</strong> Converts HP Dock's DisplayPort output to HDMI for consistent equipment chain.</div>
                            <span class="quantity">Need: 2 (one per HP Dock monitor)</span>
                        </div>
                    </div>
```

**Step 2: Verify in browser**

Check new DP to HDMI adapter card appears in equipment section

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: add DP to HDMI adapter equipment card"
```

---

## Task 3: Update Equipment Quantities

**Files:**
- Modify: `index.html:318,308,299`

**Step 1: Update BENFEI quantity**

Change line ~318:

```html
<span class="quantity">Need: 6 total (4 for MacBooks + 2 for HP Dock)</span>
```

**Step 2: Update HDMI coupler quantity**

Change line ~308:

```html
<span class="quantity">You have: 4 couplers (need 2 more for HP Dock)</span>
```

**Step 3: Update EDID quantity**

Change line ~299:

```html
<span class="quantity">Recommended: 6× 1440p (4 for MacBooks + 2 for HP Dock)</span>
```

**Step 4: Update USB-C to HDMI quantity**

Change line ~327:

```html
<span class="quantity">Need: 4 total (2 per MacBook)</span>
```

**Step 5: Verify in browser**

Check all quantities are updated correctly

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update equipment quantities for v3.0.0"
```

---

## Task 4: Add Shopping List Section

**Files:**
- Modify: `index.html:331` (after equipment grid, before Part 1)

**Step 1: Add shopping list section**

Insert new section with inventory tables:

```html
            <!-- SHOPPING LIST -->
            <div class="section" style="background: linear-gradient(135deg, #f5f5f5 0%, #e0e0e0 100%); padding: 30px; border-radius: 12px; margin-bottom: 30px;">
                <h2 style="font-size: 1.8rem; color: #1565c0; margin-bottom: 25px;">🛒 Complete Shopping List</h2>

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 25px; margin-bottom: 25px;">
                    <!-- Have Section -->
                    <div style="background: white; padding: 20px; border-radius: 10px; border-left: 5px solid #4caf50;">
                        <h3 style="color: #2e7d32; margin-bottom: 15px;">✅ Equipment You Have</h3>
                        <table style="width: 100%; font-size: 0.9rem;">
                            <tr><td>Samsung ViewFinity S65UC 34" monitors</td><td style="text-align: right; font-weight: bold;">2</td></tr>
                            <tr><td>UGREEN Revodok Pro 6-in-1 Hub</td><td style="text-align: right; font-weight: bold;">2</td></tr>
                            <tr><td>BENFEI HDMI→DP adapters</td><td style="text-align: right; font-weight: bold;">4</td></tr>
                            <tr><td>EDID 1440p emulators</td><td style="text-align: right; font-weight: bold;">2</td></tr>
                            <tr><td>EDID 1080p emulators</td><td style="text-align: right; font-weight: bold;">4</td></tr>
                            <tr><td>HDMI couplers (female-female)</td><td style="text-align: right; font-weight: bold;">4</td></tr>
                            <tr><td>USB-C to HDMI cables</td><td style="text-align: right; font-weight: bold;">2</td></tr>
                            <tr><td>DisplayPort cables</td><td style="text-align: right; font-weight: bold;">~4+</td></tr>
                        </table>
                    </div>

                    <!-- Need to Buy Section -->
                    <div style="background: white; padding: 20px; border-radius: 10px; border-left: 5px solid #ff9800;">
                        <h3 style="color: #e65100; margin-bottom: 15px;">🛒 Need to Buy</h3>
                        <table style="width: 100%; font-size: 0.9rem;">
                            <tr><td>USB-C to HDMI cables</td><td style="text-align: right; font-weight: bold;">2</td><td style="text-align: right; color: #666;">$30-40</td></tr>
                            <tr><td>EDID 1440p emulators</td><td style="text-align: right; font-weight: bold;">4</td><td style="text-align: right; color: #666;">$60-80</td></tr>
                            <tr><td>BENFEI HDMI→DP adapters</td><td style="text-align: right; font-weight: bold;">2</td><td style="text-align: right; color: #666;">$30-40</td></tr>
                            <tr><td>DP to HDMI adapters</td><td style="text-align: right; font-weight: bold;">2</td><td style="text-align: right; color: #666;">$20-30</td></tr>
                            <tr><td>HDMI couplers</td><td style="text-align: right; font-weight: bold;">2</td><td style="text-align: right; color: #666;">$10-20</td></tr>
                            <tr><td>Standard HDMI cables</td><td style="text-align: right; font-weight: bold;">4-6</td><td style="text-align: right; color: #666;">$20-60</td></tr>
                            <tr style="border-top: 2px solid #e0e0e0; font-weight: bold;"><td colspan="2" style="padding-top: 10px;">Estimated Total</td><td style="text-align: right; color: #e65100; padding-top: 10px;">$170-270</td></tr>
                        </table>
                    </div>
                </div>

                <!-- Total Inventory After Purchase -->
                <div style="background: white; padding: 20px; border-radius: 10px; border-left: 5px solid #2196f3;">
                    <h3 style="color: #1565c0; margin-bottom: 15px;">📦 Total Inventory After Purchase</h3>
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; font-size: 0.9rem;">
                        <div><strong>USB-C to HDMI cables:</strong> 4</div>
                        <div><strong>EDID 1440p emulators:</strong> 6</div>
                        <div><strong>BENFEI adapters:</strong> 6</div>
                        <div><strong>HDMI couplers:</strong> 6</div>
                        <div><strong>DP to HDMI adapters:</strong> 2</div>
                        <div><strong>Standard HDMI cables:</strong> 10-12</div>
                        <div><strong>DisplayPort cables:</strong> 6</div>
                    </div>
                </div>

                <div style="background: #fff3e0; border: 2px solid #ff9800; border-radius: 8px; padding: 15px; margin-top: 20px;">
                    <strong style="color: #e65100;">💡 Why These Changes?</strong><br>
                    <span style="color: #555;">The UGREEN hubs don't pass DDC/CI commands needed for Lunar to switch monitor inputs. Direct USB-C connections fix this while keeping Ethernet functionality.</span>
                </div>
            </div>
```

**Step 2: Verify shopping list displays correctly**

Check that all three sections (Have, Need, Total) display properly

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add comprehensive shopping list section"
```

---

## Task 5: Update Personal Mac Connection 1A (LEFT Monitor)

**Files:**
- Modify: `index.html:336-358`

**Step 1: Update connection header**

Change subtitle from "Uses UGREEN Hub" to "Direct USB-C connection":

```html
<div class="connection-header personal"><div class="connection-number personal">1A</div><div class="connection-info"><h4>Personal Mac → LEFT Monitor</h4><p>Direct USB-C connection</p></div></div>
```

**Step 2: Update equipment photos**

Remove UGREEN Hub photo, keep the rest:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" alt="USB-C to HDMI"><div class="label">USB-C→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" alt="BENFEI"><div class="label">BENFEI</div></div>
</div>
```

**Step 3: Update signal chain**

Remove UGREEN Hub from the chain:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">MacBook USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" class="chain-img" alt="Cable"> USB-C to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" class="chain-img" alt="BENFEI"> BENFEI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">DP Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor</span>
</div>
```

**Step 4: Update warning box**

Change power source reference:

```html
<div class="warning-box"><div class="icon">⚡</div><div class="text"><strong>Don't forget!</strong> BENFEI USB power → USB wall adapter or UGREEN Hub USB-A port!</div></div>
```

**Step 5: Verify in browser**

Check 1A connection shows updated chain without hub

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update Personal Mac 1A to direct USB-C connection"
```

---

## Task 6: Update Personal Mac Section - Add Ethernet Note

**Files:**
- Modify: `index.html:398` (after 1B connection, before completion box)

**Step 1: Add Ethernet hub note**

Insert note about UGREEN hub placement:

```html
                <div style="background: #e3f2fd; border: 2px solid #2196f3; border-radius: 8px; padding: 15px; margin: 20px 0;">
                    <strong style="color: #1565c0;">🌐 Ethernet Connection:</strong><br>
                    <span style="color: #555;">Plug UGREEN Hub into USB-C port 3 for Ethernet. Hub is NOT used for video (DDC/CI limitation).</span>
                </div>
```

**Step 2: Verify note appears**

Check that Ethernet note displays between connections and completion box

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: add Ethernet hub note to Personal Mac section"
```

---

## Task 7: Update Work Mac Connection 2A (LEFT Monitor)

**Files:**
- Modify: `index.html:388-410`

**Step 1: Update connection header**

Change subtitle from "Using UGREEN Hub #2" to "Direct USB-C connection":

```html
<div class="connection-header work"><div class="connection-number work">2A</div><div class="connection-info"><h4>Work Mac → LEFT Monitor</h4><p>Direct USB-C connection</p></div></div>
```

**Step 2: Update equipment photos**

Remove UGREEN Hub #2 photo:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" alt="USB-C to HDMI"><div class="label">USB-C→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" alt="BENFEI"><div class="label">BENFEI</div></div>
</div>
```

**Step 3: Update signal chain**

Remove UGREEN Hub #2:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">Work Mac USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" class="chain-img" alt="Cable"> USB-C to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" class="chain-img" alt="BENFEI"> BENFEI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">DP Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor</span>
</div>
```

**Step 4: Add Ethernet note**

Insert same Ethernet note as Personal Mac (after 2B, before completion):

```html
                <div style="background: #e3f2fd; border: 2px solid #2196f3; border-radius: 8px; padding: 15px; margin: 20px 0;">
                    <strong style="color: #1565c0;">🌐 Ethernet Connection:</strong><br>
                    <span style="color: #555;">Plug UGREEN Hub #2 into USB-C port 3 for Ethernet. Hub is NOT used for video (DDC/CI limitation).</span>
                </div>
```

**Step 5: Verify in browser**

Check 2A shows updated chain and Ethernet note appears

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update Work Mac 2A to direct USB-C connection"
```

---

## Task 8: Update HP Dock Connection 3A (LEFT Monitor)

**Files:**
- Modify: `index.html:440-450`

**Step 1: Update connection header**

Change title and subtitle:

```html
<div class="connection-header hp"><div class="connection-number hp">3A</div><div class="connection-info"><h4>HP Dock → LEFT Monitor</h4><p>DP to HDMI conversion</p></div></div>
```

**Step 2: Add equipment photos**

Add DP to HDMI adapter and full chain:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" alt="DP to HDMI"><div class="label">DP→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" alt="BENFEI"><div class="label">BENFEI</div></div>
</div>
```

**Step 3: Update signal chain**

Replace VGA chain with DP→HDMI→EDID→BENFEI→DP:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">HP Dock DP</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" class="chain-img" alt="Adapter"> DP to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">HDMI Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" class="chain-img" alt="BENFEI"> BENFEI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">DP Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor</span>
</div>
```

**Step 4: Update tip box**

Replace "Easiest Connection!" with equipment note:

```html
<div style="background: #e8f5e9; border: 2px solid #4caf50; border-radius: 8px; padding: 15px; margin: 15px 0;"><strong style="color: #2e7d32;">💡 Better Quality!</strong> DisplayPort provides better image quality than VGA.</div>
```

**Step 5: Add warning box**

Add BENFEI power warning:

```html
<div class="warning-box"><div class="icon">⚡</div><div class="text"><strong>USB Power Required!</strong> Don't forget BENFEI USB power cable.</div></div>
```

**Step 6: Verify in browser**

Check 3A shows full DP→HDMI→EDID→BENFEI chain

**Step 7: Commit**

```bash
git add index.html
git commit -m "docs: update HP Dock 3A from VGA to DP-HDMI chain"
```

---

## Task 9: Update HP Dock Connection 3B (RIGHT Monitor)

**Files:**
- Modify: `index.html:468-478`

**Step 1: Update connection header**

Change title and subtitle:

```html
<div class="connection-header hp"><div class="connection-number hp">3B</div><div class="connection-info"><h4>HP Dock → RIGHT Monitor</h4><p>Same as LEFT</p></div></div>
```

**Step 2: Add equipment photos**

Same as 3A:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" alt="DP to HDMI"><div class="label">DP→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" alt="BENFEI"><div class="label">BENFEI</div></div>
</div>
```

**Step 3: Update signal chain**

Replace VGA with full chain:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">HP Dock DP #2</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" class="chain-img" alt="Adapter"> DP to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">HDMI Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" class="chain-img" alt="BENFEI"> BENFEI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">DP Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">RIGHT Monitor</span>
</div>
```

**Step 4: Add warning box**

```html
<div class="warning-box"><div class="icon">⚡</div><div class="text"><strong>USB Power Required!</strong> Don't forget BENFEI USB power cable.</div></div>
```

**Step 5: Verify in browser**

Check 3B matches 3A configuration

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update HP Dock 3B from VGA to DP-HDMI chain"
```

---

## Task 10: Update JavaScript Wizard - Personal Mac 1A

**Files:**
- Modify: `index.html:700-729`

**Step 1: Update equipment array**

Remove UGREEN Hub from equipment list:

```javascript
equipment: [
    { name: 'USB-C to HDMI', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg', note: 'Direct cable' },
    { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Pink label' },
    { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
    { name: 'BENFEI', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg', note: 'HDMI→DP' }
],
```

**Step 2: Update detailedSteps**

Remove hub references:

```javascript
detailedSteps: [
    { text: 'Plug USB-C to HDMI cable into MacBook USB-C port', tip: 'Use port 1 for LEFT monitor' },
    { text: 'Connect HDMI end to EDID 1440p emulator', tip: 'Use 1440p for best quality' },
    { text: 'Attach Coupler to EDID output', tip: 'EDID has male output, coupler provides female connection' },
    { text: 'Connect BENFEI adapter to Coupler', tip: null },
    { text: 'Plug BENFEI USB power into USB wall adapter', tip: '⚡ CRITICAL: Won\'t work without power!' },
    { text: 'Run DP cable from BENFEI to LEFT monitor', tip: 'Use a high-quality VESA certified DP cable' }
],
```

**Step 3: Update signalChain**

Remove UGREEN Hub:

```javascript
signalChain: [
    { text: 'MacBook USB-C', class: 'chain-computer' },
    { text: 'USB-C to HDMI', class: 'chain-cable', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg' },
    { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
    { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
    { text: 'BENFEI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg' },
    { text: 'DP Cable', class: 'chain-cable' },
    { text: 'LEFT Monitor', class: 'chain-monitor' }
],
```

**Step 4: Update warning**

Update power source:

```javascript
warning: { title: 'Don\'t forget USB Power!', text: 'The BENFEI adapter requires USB power to function. Plug the USB cable into a USB wall adapter or the UGREEN Hub\'s USB-A port (hub used for Ethernet only).' }
```

**Step 5: Verify wizard**

Open wizard tab and check step 1A shows updated equipment

**Step 6: Commit**

```bash
git add index.html
git commit -m "feat: update wizard Personal Mac 1A - remove hub"
```

---

## Task 11: Update JavaScript Wizard - Work Mac 2A

**Files:**
- Modify: `index.html:765-794`

**Step 1: Update equipment array**

Same changes as Personal Mac 1A:

```javascript
equipment: [
    { name: 'USB-C to HDMI', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg', note: 'Direct cable' },
    { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Pink label' },
    { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
    { name: 'BENFEI', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg', note: 'HDMI→DP' }
],
```

**Step 2: Update detailedSteps**

```javascript
detailedSteps: [
    { text: 'Plug USB-C to HDMI cable into Work MacBook USB-C port', tip: 'Use port 1 for LEFT monitor' },
    { text: 'Connect HDMI end to EDID 1440p emulator', tip: 'Use 1440p for best quality' },
    { text: 'Attach Coupler to EDID output', tip: null },
    { text: 'Connect BENFEI adapter to Coupler', tip: null },
    { text: 'Plug BENFEI USB power into USB wall adapter', tip: '⚡ Essential for BENFEI to work!' },
    { text: 'Run DP cable from BENFEI to LEFT monitor', tip: 'Use a high-quality VESA certified DP cable' }
],
```

**Step 3: Update signalChain**

Same as Personal Mac (remove hub):

```javascript
signalChain: [
    { text: 'Work Mac USB-C', class: 'chain-computer' },
    { text: 'USB-C to HDMI', class: 'chain-cable', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg' },
    { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
    { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
    { text: 'BENFEI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg' },
    { text: 'DP Cable', class: 'chain-cable' },
    { text: 'LEFT Monitor', class: 'chain-monitor' }
],
```

**Step 4: Verify wizard**

Check Work Mac 2A shows updated configuration

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update wizard Work Mac 2A - remove hub"
```

---

## Task 12: Update JavaScript Wizard - HP Dock 3A

**Files:**
- Modify: `index.html:830-846`

**Step 1: Update title and subtitle**

```javascript
id: '3a',
title: 'LEFT Monitor',
subtitle: 'DP to HDMI conversion',
```

**Step 2: Update equipment array**

Add full equipment chain:

```javascript
equipment: [
    { name: 'DP to HDMI Adapter', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg', note: 'Converts DP to HDMI' },
    { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Pink label' },
    { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
    { name: 'BENFEI', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg', note: 'HDMI→DP' }
],
```

**Step 3: Update detailedSteps**

```javascript
detailedSteps: [
    { text: 'Locate DisplayPort output on HP Dock', tip: 'HP Dock has multiple DP ports' },
    { text: 'Connect DP to HDMI adapter to HP Dock DP port', tip: 'Converts signal to HDMI' },
    { text: 'Connect HDMI cable from adapter to EDID 1440p', tip: null },
    { text: 'Attach Coupler to EDID output', tip: null },
    { text: 'Connect BENFEI adapter to Coupler', tip: null },
    { text: 'Plug BENFEI USB power into USB wall adapter', tip: '⚡ Required for BENFEI!' },
    { text: 'Run DP cable from BENFEI to LEFT monitor', tip: 'Much better quality than VGA!' }
],
```

**Step 4: Update signalChain**

```javascript
signalChain: [
    { text: 'HP Dock DP', class: 'chain-computer' },
    { text: 'DP to HDMI Adapter', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg' },
    { text: 'HDMI Cable', class: 'chain-cable' },
    { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
    { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
    { text: 'BENFEI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg' },
    { text: 'DP Cable', class: 'chain-cable' },
    { text: 'LEFT Monitor VGA', class: 'chain-monitor' }
],
```

**Step 5: Update tip**

```javascript
tip: { title: 'Better Quality!', text: 'DisplayPort provides much better image quality than the old VGA connection.' }
```

**Step 6: Verify wizard**

Check HP Dock 3A shows new DP→HDMI chain

**Step 7: Commit**

```bash
git add index.html
git commit -m "feat: update wizard HP Dock 3A - DP to HDMI chain"
```

---

## Task 13: Update JavaScript Wizard - HP Dock 3B

**Files:**
- Modify: `index.html:867-883`

**Step 1: Update title and subtitle**

```javascript
id: '3b',
title: 'RIGHT Monitor',
subtitle: 'Same as LEFT',
```

**Step 2: Copy 3A configuration**

Use identical equipment, steps, and chain as 3A (just change port number):

```javascript
equipment: [
    { name: 'DP to HDMI Adapter', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg', note: 'Converts DP to HDMI' },
    { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Pink label' },
    { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
    { name: 'BENFEI', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg', note: 'HDMI→DP' }
],
detailedSteps: [
    { text: 'Locate second DisplayPort output on HP Dock', tip: 'Use a different DP port than LEFT' },
    { text: 'Connect DP to HDMI adapter to HP Dock DP port', tip: null },
    { text: 'Connect HDMI cable from adapter to EDID 1440p', tip: null },
    { text: 'Attach Coupler to EDID output', tip: null },
    { text: 'Connect BENFEI adapter to Coupler', tip: null },
    { text: 'Plug BENFEI USB power into USB wall adapter', tip: '⚡ Required for BENFEI!' },
    { text: 'Run DP cable from BENFEI to RIGHT monitor', tip: 'Consistent quality on both monitors!' }
],
signalChain: [
    { text: 'HP Dock DP #2', class: 'chain-computer' },
    { text: 'DP to HDMI Adapter', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg' },
    { text: 'HDMI Cable', class: 'chain-cable' },
    { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
    { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
    { text: 'BENFEI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg' },
    { text: 'DP Cable', class: 'chain-cable' },
    { text: 'RIGHT Monitor VGA', class: 'chain-monitor' }
],
tip: { title: 'Simple and Done!', text: 'Same setup as LEFT - consistent equipment makes troubleshooting easier!' }
```

**Step 3: Verify wizard**

Check HP Dock 3B matches 3A

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: update wizard HP Dock 3B - DP to HDMI chain"
```

---

## Task 14: Update Software Setup Section - DDC/CI Note

**Files:**
- Modify: `index.html:480-541`

**Step 1: Add DDC/CI explanation**

Find the Software Setup Guide section and add explanation before the link:

```html
                <div style="background: #fff3e0; border: 2px solid #ff9800; border-radius: 12px; padding: 20px; margin-bottom: 25px;">
                    <h3 style="color: #e65100; margin-bottom: 15px;">⚠️ Important: Why Direct Connections?</h3>
                    <p style="color: #555; line-height: 1.6;">
                        <strong>DDC/CI (Display Data Channel Command Interface)</strong> is required for Lunar to switch monitor inputs automatically.
                        The UGREEN hubs block these commands when video passes through them, which is why we use <strong>direct USB-C to HDMI connections</strong> for the MacBooks.
                    </p>
                    <p style="color: #555; line-height: 1.6; margin-top: 10px;">
                        The UGREEN hubs are still used for <strong>Ethernet only</strong> - plug them into USB-C port 3 on each MacBook.
                    </p>
                </div>
```

**Step 2: Verify note displays**

Check that DDC/CI explanation appears in software section

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: add DDC/CI explanation to software section"
```

---

## Task 15: Update CHANGELOG and Version to 3.0.0

**Files:**
- Modify: `CHANGELOG.md`
- Modify: `README.md`

**Step 1: Update CHANGELOG**

Add v3.0.0 entry at the top:

```markdown
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
...
```

**Step 2: Update README**

Update version reference:

```markdown
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
...
```

**Step 3: Commit**

```bash
git add CHANGELOG.md README.md
git commit -m "docs: update changelog and README for v3.0.0"
```

---

## Task 16: Deploy to Vercel

**Files:**
- Modify: `public/index.html`

**Step 1: Copy updated file to public directory**

```bash
cp index.html public/index.html
```

**Step 2: Verify file**

```bash
ls -lh public/index.html
```

Expected: File exists and is recent

**Step 3: Commit deployment file**

```bash
git add public/index.html
git commit -m "deploy: v3.0.0 with DDC/CI fix and shopping list"
```

**Step 4: Deploy to Vercel**

```bash
vercel --prod
```

Expected: Deployment succeeds, returns production URL

**Step 5: Verify live site**

Visit https://vercel-kvm.vercel.app/ and verify:
- Shopping list section appears with all three tables
- Personal Mac and Work Mac show direct USB-C connections (no hub in video chain)
- HP Dock shows DP→HDMI→EDID→BENFEI→DP chain (not VGA)
- Equipment section shows updated quantities
- Wizard reflects all changes
- DDC/CI explanation appears in software section

---

## Task 17: Create Git Tag for v3.0.0

**Files:**
- N/A (git tag only)

**Step 1: Create annotated tag**

```bash
git tag -a v3.0.0 -m "Version 3.0.0: DDC/CI fix with direct connections and comprehensive shopping list"
```

**Step 2: Push tag to remote**

```bash
git push origin v3.0.0
```

Expected: Tag pushed successfully

**Step 3: Verify on GitHub**

Visit https://github.com/chaceholland/kvm-setup-guide/releases/tag/v3.0.0

Expected: Release tag visible with description

---

## Execution Notes

- **Total estimated time:** 120-150 minutes
- **Dependencies:** None (static HTML project)
- **Testing:** Manual browser testing after each section update
- **Rollback:** Use `git revert` if issues occur

## Success Criteria

- ✅ All MacBook connections show direct USB-C (no hub in video path)
- ✅ HP Dock connections use DP→HDMI conversion (not VGA)
- ✅ Shopping list displays with accurate inventory counts
- ✅ Equipment quantities updated correctly
- ✅ DDC/CI explanation added to software section
- ✅ All wizard data reflects new connections
- ✅ Live site deployed successfully
- ✅ Version tagged as v3.0.0
