# KVM Guide Corrected Monitor Inputs Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Update the KVM guide to reflect correct monitor input configuration where each computer uses a different input type (HDMI, DP, USB-C) on both monitors.

**Architecture:** Update single-file HTML guide to change connection diagrams and signal chains. Personal Mac uses HDMI, Work Mac uses DisplayPort, HP Dock uses USB-C. Update equipment lists, wizard data, and software references.

**Tech Stack:** Static HTML/CSS/JavaScript, Better Display, InputLeap, deployed to Vercel

---

## Task 1: Update Personal Mac Connections (HDMI)

**Files:**
- Modify: `index.html:399-451` (Personal Mac section)

**Step 1: Update Personal Mac LEFT monitor connection**

Change connection 1A from current setup to HDMI-only:

```html
<div class="connection-header personal">
    <div class="connection-number personal">1A</div>
    <div class="connection-info">
        <h4>Personal Mac → LEFT Monitor</h4>
        <p>Direct HDMI via USB-C cable</p>
    </div>
</div>
```

Update signal chain to:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">MacBook USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" class="chain-img" alt="Cable"> USB-C to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor HDMI</span>
</div>
```

Remove BENFEI and coupler references from inline photos.

**Step 2: Update Personal Mac RIGHT monitor connection**

Update 1B with same HDMI-only pattern:

```html
<div class="connection-header personal">
    <div class="connection-number personal">1B</div>
    <div class="connection-info">
        <h4>Personal Mac → RIGHT Monitor</h4>
        <p>Direct HDMI via USB-C cable</p>
    </div>
</div>
```

Signal chain:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">MacBook USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" class="chain-img" alt="Cable"> USB-C to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">RIGHT Monitor HDMI</span>
</div>
```

**Step 3: Add note about simplicity**

Add info box after 1B:

```html
<div style="background: #e8f5e9; border: 2px solid #4caf50; border-radius: 8px; padding: 15px; margin: 15px 0;">
    <strong style="color: #2e7d32;">✨ Simplest Setup!</strong><br>
    <span style="color: #555;">Personal Mac has the cleanest connection: USB-C cable → EDID → Monitor HDMI. No extra adapters!</span>
</div>
```

**Step 4: Verify changes in browser**

Open `index.html` and check Personal Mac section shows HDMI-only connections

**Step 5: Commit**

```bash
git add index.html
git commit -m "docs: update Personal Mac to use HDMI inputs on both monitors"
```

---

## Task 2: Update Work Mac Connections (DisplayPort)

**Files:**
- Modify: `index.html:453-505` (Work Mac section)

**Step 1: Update Work Mac LEFT monitor connection (2A)**

Change to DisplayPort with BENFEI adapter:

```html
<div class="connection-header work">
    <div class="connection-number work">2A</div>
    <div class="connection-info">
        <h4>Work Mac → LEFT Monitor</h4>
        <p>DisplayPort via BENFEI adapter</p>
    </div>
</div>
```

Update inline photos to include coupler and BENFEI:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" alt="USB-C to HDMI"><div class="label">USB-C→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" alt="BENFEI"><div class="label">BENFEI</div></div>
</div>
```

Signal chain:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">Work Mac USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable"><img src="https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg" class="chain-img" alt="Cable"> USB-C to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg" class="chain-img" alt="BENFEI"> BENFEI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">DP Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor DisplayPort</span>
</div>
```

Add USB power warning:

```html
<div class="warning-box">
    <div class="icon">⚡</div>
    <div class="text"><strong>USB Power Required!</strong> Connect BENFEI USB power cable to wall adapter or USB port.</div>
</div>
```

**Step 2: Update Work Mac RIGHT monitor connection (2B)**

Same pattern as 2A but for RIGHT monitor:

```html
<div class="connection-header work">
    <div class="connection-number work">2B</div>
    <div class="connection-info">
        <h4>Work Mac → RIGHT Monitor</h4>
        <p>DisplayPort via BENFEI adapter</p>
    </div>
</div>
```

Same signal chain and warnings as 2A, pointing to RIGHT Monitor DisplayPort.

**Step 3: Verify Work Mac section**

Check both connections show DisplayPort with BENFEI adapters

**Step 4: Commit**

```bash
git add index.html
git commit -m "docs: update Work Mac to use DisplayPort inputs with BENFEI adapters"
```

---

## Task 3: Update HP Dock Connections (USB-C)

**Files:**
- Modify: `index.html:507-560` (HP Dock section)

**Step 1: Update HP Dock LEFT monitor connection (3A)**

Change to USB-C with DP→HDMI and HDMI→USB-C adapters:

```html
<div class="connection-header hp">
    <div class="connection-number hp">3A</div>
    <div class="connection-info">
        <h4>HP Dock → LEFT Monitor</h4>
        <p>USB-C via DP→HDMI→USB-C conversion</p>
    </div>
</div>
```

Update inline photos:

```html
<div class="inline-photos">
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" alt="DP to HDMI"><div class="label">DP→HDMI</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" alt="EDID"><div class="label">EDID 1440p</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" alt="Coupler"><div class="label">Coupler</div></div>
    <div class="inline-photo"><img src="https://m.media-amazon.com/images/I/61B3vXOGRiL._AC_SL1500_.jpg" alt="HDMI to USB-C"><div class="label">HDMI→USB-C</div></div>
</div>
```

Signal chain:

```html
<div class="signal-chain">
    <span class="chain-item chain-computer">HP Dock DP</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg" class="chain-img" alt="Adapter"> DP to HDMI</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-cable">HDMI Cable</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-edid"><img src="https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg" class="chain-img" alt="EDID"> EDID 1440p</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-coupler"><img src="https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg" class="chain-img" alt="Coupler"> Coupler</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-adapter"><img src="https://m.media-amazon.com/images/I/61B3vXOGRiL._AC_SL1500_.jpg" class="chain-img" alt="Adapter"> HDMI to USB-C</span><span class="chain-arrow">→</span>
    <span class="chain-item chain-monitor">LEFT Monitor USB-C</span>
</div>
```

**Step 2: Update HP Dock RIGHT monitor connection (3B)**

Same pattern pointing to RIGHT Monitor USB-C.

**Step 3: Add note about adapter chain**

```html
<div style="background: #fff3e0; border: 2px solid #ff9800; border-radius: 8px; padding: 15px; margin: 15px 0;">
    <strong style="color: #e65100;">ℹ️ Two-Stage Conversion</strong><br>
    <span style="color: #555;">HP Dock uses two adapters per monitor (DP→HDMI then HDMI→USB-C) to reach the USB-C input while maintaining EDID in the chain.</span>
</div>
```

**Step 4: Verify HP Dock section**

Check both connections show USB-C with two-stage conversion

**Step 5: Commit**

```bash
git add index.html
git commit -m "docs: update HP Dock to use USB-C inputs with dual conversion"
```

---

## Task 4: Update Equipment Overview Section

**Files:**
- Modify: `index.html:280-395` (Equipment section)

**Step 1: Add HDMI to USB-C adapter card**

After the DP to HDMI adapter card (line ~338), add:

```html
<div class="equipment-card">
    <div class="card-header" style="background: linear-gradient(135deg, #673ab7 0%, #512da8 100%);">🔌 HDMI to USB-C Adapter</div>
    <div class="card-body">
        <div class="photo-container"><img src="https://m.media-amazon.com/images/I/61B3vXOGRiL._AC_SL1500_.jpg" alt="HDMI to USB-C Adapter"></div>
        <div class="port-labels"><span class="port-label hdmi">HDMI IN (Male)</span><span class="port-label usb">USB-C OUT</span></div>
        <div class="description"><strong>What it does:</strong> Converts HDMI signal from EDID output to USB-C for monitor USB-C input (HP Dock).</div>
        <span class="quantity">Need: 2 (one per HP Dock monitor)</span>
    </div>
</div>
```

**Step 2: Update shopping list (Have section)**

Update line ~351-359:

```html
<h3 style="color: #2e7d32; margin-bottom: 15px;">✅ Equipment You Have</h3>
<table style="width: 100%; font-size: 0.9rem;">
    <tr><td>Samsung ViewFinity S65UC 34" monitors</td><td style="text-align: right; font-weight: bold;">2</td></tr>
    <tr><td>UGREEN Revodok Pro 6-in-1 Hub</td><td style="text-align: right; font-weight: bold;">2</td></tr>
    <tr><td>EDID 1440p emulators</td><td style="text-align: right; font-weight: bold;">6</td></tr>
    <tr><td>HDMI couplers (female-female)</td><td style="text-align: right; font-weight: bold;">6</td></tr>
    <tr><td>USB-C to HDMI cables</td><td style="text-align: right; font-weight: bold;">4</td></tr>
    <tr><td>DisplayPort cables</td><td style="text-align: right; font-weight: bold;">2+</td></tr>
</table>
```

**Step 3: Update shopping list (Need to Buy section)**

Update line ~365-375:

```html
<h3 style="color: #c62828; margin-bottom: 15px;">🛒 Need to Buy</h3>
<table style="width: 100%; font-size: 0.9rem;">
    <tr><td>BENFEI HDMI→DP adapters (with USB power)</td><td style="text-align: right; font-weight: bold;">4</td></tr>
    <tr><td>DP to HDMI adapters</td><td style="text-align: right; font-weight: bold;">2</td></tr>
    <tr><td>HDMI to USB-C adapters</td><td style="text-align: right; font-weight: bold;">2</td></tr>
    <tr style="border-top: 2px solid #ddd;"><td colspan="2" style="padding-top: 10px; font-style: italic; color: #666;">Total new items needed: 8 adapters</td></tr>
</table>
```

**Step 4: Verify equipment section**

Check all equipment cards present and shopping lists updated

**Step 5: Commit**

```bash
git add index.html
git commit -m "docs: update equipment section with HDMI→USB-C adapter and counts"
```

---

## Task 5: Update Better Display Configuration Instructions

**Files:**
- Modify: `index.html:564-650` (Software section)

**Step 1: Update Better Display hotkey instructions**

Find and update the hotkey configuration text (around line ~620):

```html
<tr>
    <td style="padding: 10px;"><strong>Better Display (DDC/CI)</strong></td>
    <td style="padding: 10px;">
        Cmd+1: Switch both monitors to HDMI (Personal Mac)<br>
        Cmd+2: Switch both monitors to DisplayPort (Work Mac)<br>
        Cmd+3: Switch both monitors to USB-C (HP Dock)
    </td>
</tr>
```

**Step 2: Update DDC/CI explanation**

Update the warning box explaining input types (around line ~574):

```html
<div style="background: #fff3e0; border: 2px solid #ff9800; border-radius: 12px; padding: 20px; margin-bottom: 25px;">
    <h3 style="color: #e65100; margin-bottom: 15px;">⚠️ Important: Input Type Assignment</h3>
    <p style="color: #555; line-height: 1.6;">
        <strong>Each computer uses a different input type:</strong><br>
        • Personal Mac → HDMI (simplest, no extra adapters)<br>
        • Work Mac → DisplayPort (via BENFEI HDMI→DP adapter)<br>
        • HP Dock → USB-C (via DP→HDMI→USB-C conversion)
    </p>
    <p style="color: #555; line-height: 1.6; margin-top: 10px;">
        Better Display uses DDC/CI to switch both monitors to the same input type simultaneously with one hotkey press.
    </p>
</div>
```

**Step 3: Verify software section**

Check Better Display instructions reflect correct input mappings

**Step 4: Commit**

```bash
git add index.html
git commit -m "docs: update Better Display config for HDMI/DP/USB-C inputs"
```

---

## Task 6: Update Wizard Completion Screen

**Files:**
- Modify: `index.html:756-782` (Wizard completion)

**Step 1: Update hardware summary table**

Update the connection summary (line ~763-768):

```html
<table class="summary-table">
    <thead><tr><th>Computer</th><th>LEFT</th><th>RIGHT</th></tr></thead>
    <tbody>
        <tr><td>🟢 Personal</td><td>USB-C→HDMI input</td><td>USB-C→HDMI input</td></tr>
        <tr><td>🟠 Work</td><td>USB-C→BENFEI→DP input</td><td>USB-C→BENFEI→DP input</td></tr>
        <tr><td>🟣 HP Dock</td><td>DP→HDMI→USB-C input</td><td>DP→HDMI→USB-C input</td></tr>
    </tbody>
</table>
```

**Step 2: Update footer help text**

Update line ~779:

```html
<p style="margin-top: 15px; font-size: 0.9rem; color: #aaa;">
    InputLeap: Move mouse to edge to switch computers | Better Display: Cmd+1=HDMI, Cmd+2=DP, Cmd+3=USB-C
</p>
```

**Step 3: Verify completion screen**

Check table shows correct input types for each computer

**Step 4: Commit**

```bash
git add index.html
git commit -m "docs: update wizard completion screen with correct inputs"
```

---

## Task 7: Update JavaScript Wizard Data - Personal Mac

**Files:**
- Modify: `index.html:800-867` (wizardData.personal)

**Step 1: Update step 1a (Personal Mac LEFT)**

Change equipment and signal chain:

```javascript
{
    id: '1a',
    title: 'LEFT Monitor',
    subtitle: 'HDMI via USB-C cable',
    equipment: [
        { name: 'USB-C to HDMI', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg', note: 'Direct cable' },
        { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Blue label' }
    ],
    detailedSteps: [
        { text: 'Plug USB-C to HDMI cable into MacBook', tip: 'Use any available USB-C port' },
        { text: 'Connect HDMI end to EDID 1440p', tip: 'EDID male connector fits into cable female HDMI' },
        { text: 'Connect EDID output directly to monitor HDMI input', tip: 'EDID male output goes straight to monitor - no coupler needed!' }
    ],
    signalChain: [
        { text: 'MacBook USB-C', class: 'chain-computer' },
        { text: 'USB-C to HDMI', class: 'chain-cable', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg' },
        { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
        { text: 'LEFT Monitor HDMI', class: 'chain-monitor' }
    ],
    tip: { title: 'Simplest Setup!', text: 'Personal Mac has the cleanest connection with no extra adapters after EDID.' }
}
```

**Step 2: Update step 1b (Personal Mac RIGHT)**

Same pattern for RIGHT monitor:

```javascript
{
    id: '1b',
    title: 'RIGHT Monitor',
    subtitle: 'HDMI via USB-C cable',
    equipment: [
        { name: 'USB-C to HDMI', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg', note: 'Direct cable' },
        { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Blue label' }
    ],
    detailedSteps: [
        { text: 'Plug USB-C to HDMI cable into MacBook', tip: 'Use different port than LEFT monitor' },
        { text: 'Connect HDMI end to EDID 1440p', tip: null },
        { text: 'Connect EDID output directly to monitor HDMI input', tip: 'No coupler needed!' }
    ],
    signalChain: [
        { text: 'MacBook USB-C', class: 'chain-computer' },
        { text: 'USB-C to HDMI', class: 'chain-cable', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg' },
        { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
        { text: 'RIGHT Monitor HDMI', class: 'chain-monitor' }
    ],
    tip: { title: 'Quick Setup!', text: 'Same simple pattern as LEFT monitor.' }
}
```

**Step 3: Verify Personal Mac wizard data**

Check both steps show HDMI-only connections

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: update Personal Mac wizard data for HDMI connections"
```

---

## Task 8: Update JavaScript Wizard Data - Work Mac

**Files:**
- Modify: `index.html:869-930` (wizardData.work)

**Step 1: Update step 2a (Work Mac LEFT)**

Add BENFEI and coupler to equipment and chain:

```javascript
{
    id: '2a',
    title: 'LEFT Monitor',
    subtitle: 'DisplayPort via BENFEI',
    equipment: [
        { name: 'USB-C to HDMI', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg', note: 'Direct cable' },
        { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Blue label' },
        { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
        { name: 'BENFEI', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg', note: 'HDMI→DP' }
    ],
    detailedSteps: [
        { text: 'Plug USB-C to HDMI cable into Work MacBook', tip: null },
        { text: 'Connect HDMI end to EDID 1440p', tip: null },
        { text: 'Attach Coupler to EDID output', tip: 'EDID male output needs coupler to connect to BENFEI male input' },
        { text: 'Connect BENFEI adapter to Coupler', tip: 'HDMI IN side goes to coupler' },
        { text: 'Plug BENFEI USB power cable', tip: '⚡ CRITICAL: BENFEI requires USB power to work!' },
        { text: 'Run DP cable from BENFEI to LEFT monitor DP input', tip: 'Use high-quality DisplayPort cable' }
    ],
    signalChain: [
        { text: 'Work Mac USB-C', class: 'chain-computer' },
        { text: 'USB-C to HDMI', class: 'chain-cable', img: 'https://m.media-amazon.com/images/I/61dPxJI54+L._AC_SL1393_.jpg' },
        { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
        { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
        { text: 'BENFEI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61epo1+QzrL._SL1500_.jpg' },
        { text: 'DP Cable', class: 'chain-cable' },
        { text: 'LEFT Monitor DP', class: 'chain-monitor' }
    ],
    warning: { title: 'USB Power Required!', text: 'BENFEI adapter must have USB power connected to function.' }
}
```

**Step 2: Update step 2b (Work Mac RIGHT)**

Same pattern for RIGHT monitor DisplayPort.

**Step 3: Verify Work Mac wizard data**

Check both steps include BENFEI adapters and DP connections

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: update Work Mac wizard data for DisplayPort via BENFEI"
```

---

## Task 9: Update JavaScript Wizard Data - HP Dock

**Files:**
- Modify: `index.html:932-998` (wizardData.hp)

**Step 1: Update step 3a (HP Dock LEFT)**

Add both conversion adapters:

```javascript
{
    id: '3a',
    title: 'LEFT Monitor',
    subtitle: 'USB-C via dual conversion',
    equipment: [
        { name: 'DP to HDMI', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg', note: 'First adapter' },
        { name: 'EDID 1440p', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg', note: 'Blue label' },
        { name: 'Coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg', note: 'Female-Female' },
        { name: 'HDMI to USB-C', img: 'https://m.media-amazon.com/images/I/61B3vXOGRiL._AC_SL1500_.jpg', note: 'Second adapter' }
    ],
    detailedSteps: [
        { text: 'Connect DP to HDMI adapter to HP Dock DisplayPort output', tip: 'Use one of the two DP ports on dock' },
        { text: 'Run HDMI cable from adapter to EDID 1440p', tip: 'Short cable works if dock is close' },
        { text: 'Attach Coupler to EDID output', tip: null },
        { text: 'Connect HDMI to USB-C adapter to Coupler', tip: 'Final conversion to USB-C for monitor' },
        { text: 'Plug USB-C end into LEFT monitor USB-C input', tip: 'Monitor can provide power to adapter' }
    ],
    signalChain: [
        { text: 'HP Dock DP', class: 'chain-computer' },
        { text: 'DP to HDMI', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61Zp8vY5gYL._AC_SL1500_.jpg' },
        { text: 'HDMI Cable', class: 'chain-cable' },
        { text: 'EDID 1440p', class: 'chain-edid', img: 'https://m.media-amazon.com/images/I/512Jgn92IEL._AC_SX679_.jpg' },
        { text: 'Coupler', class: 'chain-coupler', img: 'https://m.media-amazon.com/images/I/717oGK8uZOL._AC_SL1500_.jpg' },
        { text: 'HDMI to USB-C', class: 'chain-adapter', img: 'https://m.media-amazon.com/images/I/61B3vXOGRiL._AC_SL1500_.jpg' },
        { text: 'LEFT Monitor USB-C', class: 'chain-monitor' }
    ],
    tip: { title: 'Two-Stage Conversion', text: 'HP Dock requires two adapters to go from DP → HDMI → USB-C while keeping EDID inline.' }
}
```

**Step 2: Update step 3b (HP Dock RIGHT)**

Same pattern for RIGHT monitor USB-C.

**Step 3: Verify HP Dock wizard data**

Check both steps show dual conversion to USB-C

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: update HP Dock wizard data for USB-C via dual conversion"
```

---

## Task 10: Update JavaScript Wizard Data - Software

**Files:**
- Modify: `index.html:1000-1090` (wizardData.software)

**Step 1: Update Better Display hotkey configuration step**

Find step 4b and update hotkey instructions:

```javascript
detailedSteps: [
    { text: 'Open Better Display Preferences (Cmd+,)', tip: null },
    { text: 'Go to "Hotkeys" tab', tip: null },
    { text: 'Find "Input Source" section', tip: 'This controls monitor input switching' },
    { text: 'Set Cmd+1 to switch both monitors to HDMI (Personal Mac)', tip: 'Both monitors switch to HDMI input' },
    { text: 'Set Cmd+2 to switch both monitors to DisplayPort (Work Mac)', tip: 'Both monitors switch to DP input' },
    { text: 'Set Cmd+3 to switch both monitors to USB-C (HP Dock)', tip: 'Both monitors switch to USB-C input' },
    { text: 'Test each hotkey to verify switching works', tip: 'Press Cmd+1/2/3 and watch monitors change inputs' }
]
```

**Step 2: Update final test step**

Update step 4d test instructions:

```javascript
detailedSteps: [
    { text: 'Press Cmd+1 - Both monitors should switch to HDMI (Personal Mac)', tip: 'If not working, check Better Display permissions and DDC/CI' },
    { text: 'Press Cmd+2 - Both monitors should switch to DP (Work Mac)', tip: 'Check BENFEI USB power if not working' },
    { text: 'Press Cmd+3 - Both monitors should switch to USB-C (HP Dock)', tip: 'Verify both adapters connected properly' },
    { text: 'Move mouse to screen edge - Cursor moves to other computer via InputLeap', tip: 'Verify keyboard works on the other computer too' },
    { text: 'Unplug and replug a display cable - Windows stay in place!', tip: 'EDID emulators prevent window rearranging' },
    { text: '🎉 Celebrate - Your KVM setup is complete!', tip: null }
]
```

**Step 3: Verify software wizard data**

Check hotkey descriptions match HDMI/DP/USB-C assignments

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: update software wizard data for HDMI/DP/USB-C inputs"
```

---

## Task 11: Update Final Summary Tables

**Files:**
- Modify: `index.html:650-665` (Final summary section)

**Step 1: Update connection summary table**

Update the table showing all connections:

```html
<thead>
    <tr style="background: rgba(255,255,255,0.1);">
        <th style="padding: 15px; text-align: left; border-bottom: 2px solid #4fc3f7;">Computer</th>
        <th style="padding: 15px; text-align: center; border-bottom: 2px solid #4fc3f7;">→ LEFT</th>
        <th style="padding: 15px; text-align: center; border-bottom: 2px solid #4fc3f7;">→ RIGHT</th>
    </tr>
</thead>
<tbody>
    <tr style="background: rgba(76,175,80,0.2);">
        <td style="padding: 12px; font-weight: bold;">🟢 Personal Mac</td>
        <td style="padding: 12px; text-align: center;">USB-C→HDMI input</td>
        <td style="padding: 12px; text-align: center;">USB-C→HDMI input</td>
    </tr>
    <tr style="background: rgba(255,152,0,0.2);">
        <td style="padding: 12px; font-weight: bold;">🟠 Work Mac</td>
        <td style="padding: 12px; text-align: center;">USB-C→BENFEI→DP input</td>
        <td style="padding: 12px; text-align: center;">USB-C→BENFEI→DP input</td>
    </tr>
    <tr style="background: rgba(156,39,176,0.2);">
        <td style="padding: 12px; font-weight: bold;">🟣 HP Dock</td>
        <td style="padding: 12px; text-align: center;">DP→HDMI→USB-C input</td>
        <td style="padding: 12px; text-align: center;">DP→HDMI→USB-C input</td>
    </tr>
</tbody>
```

**Step 2: Verify final summary**

Check summary table shows correct input types

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: update final summary table with correct input types"
```

---

## Task 12: Deploy to Vercel

**Files:**
- Modify: `public/index.html`

**Step 1: Copy updated file**

```bash
cp index.html public/index.html
```

**Step 2: Verify file**

```bash
ls -lh public/index.html
```

Expected: File exists and timestamp is recent

**Step 3: Test locally**

Open `public/index.html` in browser and verify:
- Personal Mac shows HDMI connections
- Work Mac shows DisplayPort with BENFEI
- HP Dock shows USB-C with dual conversion
- Equipment section has HDMI→USB-C adapter
- Better Display shows Cmd+1=HDMI, Cmd+2=DP, Cmd+3=USB-C

**Step 4: Commit deployment**

```bash
git add public/index.html
git commit -m "deploy: corrected monitor input configuration"
```

**Step 5: Deploy to Vercel**

```bash
vercel --prod
```

Expected: Deployment succeeds, returns production URL

**Step 6: Verify live site**

Visit https://vercel-kvm.vercel.app/ and verify all changes are live

---

## Task 13: Update Documentation

**Files:**
- Modify: `CHANGELOG.md`
- Modify: `README.md`

**Step 1: Update CHANGELOG**

Add new version entry:

```markdown
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
```

**Step 2: Update README**

Update monitor input details:

```markdown
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

## Version
Current version: 3.0.0 (corrected monitor inputs)
```

**Step 3: Commit documentation**

```bash
git add CHANGELOG.md README.md
git commit -m "docs: update changelog and README for v3.0.0 corrected inputs"
```

**Step 4: Create version tag**

```bash
git tag -a v3.0.0 -m "Version 3.0.0: Corrected monitor input configuration (HDMI/DP/USB-C)"
git push origin main
git push origin v3.0.0
```

---

## Execution Notes

- **Estimated time:** 2-3 hours
- **Testing:** Open in browser after each task to verify changes
- **Equipment impact:** Users will need to purchase HDMI→USB-C adapters
- **Breaking change:** Previous setup instructions are incorrect, complete rework needed

## Rollback Plan

If issues occur:
```bash
git log --oneline
git revert <commit-hash>
vercel --prod
```

Or revert to v2.0.0:
```bash
git reset --hard v2.0.0
vercel --prod
```
