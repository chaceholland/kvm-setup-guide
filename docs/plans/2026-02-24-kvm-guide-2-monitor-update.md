# KVM Guide 2-Monitor Update Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Update the KVM setup guide from 3 monitors to 2 Samsung ViewFinity S65UC 34" monitors with simplified DisplayPort connections.

**Architecture:** Single-file HTML update targeting both static content (guide sections) and dynamic JavaScript (wizard data). Remove all CENTER monitor references, relabel RIGHT→RIGHT and LEFT→LEFT, update equipment specifications, and adjust step counts throughout.

**Tech Stack:** Static HTML/CSS/JavaScript (no build process), deployed to Vercel

---

## Task 1: Update Page Header and Metadata

**Files:**
- Modify: `index.html:256-258`

**Step 1: Update header text from 3 to 2 monitors**

Find and replace in header section:

```html
<div class="header">
    <h1>🖥️ KVM Setup Guide</h1>
    <p>Step-by-Step Visual Instructions for Connecting 3 Computers to 2 Monitors</p>
    <p style="margin-top: 10px; color: #4fc3f7;">Created for Chace • January 2026</p>
</div>
```

**Step 2: Verify changes in browser**

Open `index.html` in browser and verify header reads "2 Monitors"

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: update header to reflect 2 monitors"
```

---

## Task 2: Update Table of Contents

**Files:**
- Modify: `index.html:269-276`

**Step 1: Update TOC descriptions**

Replace the TOC grid content:

```html
<div class="toc-grid">
    <div class="toc-item overview"><strong>Part 0:</strong> Equipment Overview<br><small>Photos and descriptions of each piece</small></div>
    <div class="toc-item personal"><strong>Part 1:</strong> Personal MacBook Setup<br><small>2 connections to LEFT and RIGHT monitors</small></div>
    <div class="toc-item work"><strong>Part 2:</strong> Work MacBook Setup<br><small>2 connections to LEFT and RIGHT monitors</small></div>
    <div class="toc-item hp"><strong>Part 3:</strong> HP Dock Setup<br><small>2 connections to LEFT and RIGHT monitors</small></div>
</div>
```

**Step 2: Verify in browser**

Check that TOC shows "2 connections to LEFT and RIGHT monitors"

**Step 3: Commit**

```bash
git add index.html
git commit -m "docs: update TOC for 2-monitor setup"
```

---

## Task 3: Update Equipment Overview - Remove HDMI Switch

**Files:**
- Modify: `index.html:330-338`

**Step 1: Remove HDMI switch equipment card**

Delete the entire HDMI switch equipment card section (lines ~330-338):

```html
<!-- DELETE THIS ENTIRE BLOCK -->
<div class="equipment-card">
    <div class="card-header" style="background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);">🔀 HDMI Switch</div>
    <div class="card-body">
        <div class="photo-container"><img src="https://m.media-amazon.com/images/I/61++s0S292L._AC_SL1500_.jpg" alt="HDMI Switch"></div>
        <div class="port-labels"><span class="port-label hdmi">IN1: Work</span><span class="port-label hdmi">IN2: HP</span><span class="port-label hdmi">OUT</span></div>
        <div class="warning-box"><div class="icon">🔀</div><div class="text"><strong>Use:</strong> Press button to toggle Work Mac ↔ HP Dock on CENTER monitor.</div></div>
        <span class="quantity">You have: 1 switch</span>
    </div>
</div>
```

**Step 2: Update BENFEI adapter description**

Change "ViewSonic monitors" to "Samsung ViewFinity monitors" in BENFEI card (line ~317):

```html
<div class="description"><strong>What it does:</strong> Converts HDMI to DisplayPort for Samsung ViewFinity monitors.</div>
```

**Step 3: Update BENFEI quantity**

Change quantity from "Need: 4" to "Need: 2-4" (line ~318):

```html
<span class="quantity">Need: 2-4 (depending on connection method)</span>
```

**Step 4: Verify equipment section**

Check that HDMI switch is gone and monitor references are updated

**Step 5: Commit**

```bash
git add index.html
git commit -m "docs: remove HDMI switch, update equipment for 2 monitors"
```

---

## Task 4: Update Personal Mac Section - Remove CENTER (1B)

**Files:**
- Modify: `index.html:342-410`

**Step 1: Update section header**

Change section header subtitle (line ~344):

```html
<div class="section-header personal">
    <div class="section-number personal">1</div>
    <div class="section-title">
        <h2>Personal MacBook Setup</h2>
        <p>Connect to LEFT and RIGHT monitors</p>
    </div>
</div>
```

**Step 2: Keep 1A (LEFT Monitor) unchanged**

Leave connection 1A as-is (lines ~346-367)

**Step 3: Delete 1B (CENTER Monitor) completely**

Delete the entire 1B connection guide section (lines ~368-385):

```html
<!-- DELETE THIS ENTIRE 1B SECTION -->
<div class="connection-guide">
    <div class="connection-header personal">...</div>
    ...CENTER Monitor...
</div>
```

**Step 4: Relabel 1C to 1B and update title**

Change 1C header to 1B (line ~387):

```html
<div class="connection-header personal">
    <div class="connection-number personal">1B</div>
    <div class="connection-info">
        <h4>Personal Mac → RIGHT Monitor</h4>
        <p>USB-C to HDMI cable</p>
    </div>
</div>
```

**Step 5: Verify Personal Mac section**

Check that only 1A (LEFT) and 1B (RIGHT) exist, CENTER is gone

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update Personal Mac section to 2 monitors (LEFT, RIGHT)"
```

---

## Task 5: Update Work Mac Section - Remove CENTER (2B)

**Files:**
- Modify: `index.html:415-476`

**Step 1: Update section header**

Change section header subtitle (line ~415):

```html
<div class="section-header work">
    <div class="section-number work">2</div>
    <div class="section-title">
        <h2>Work MacBook Setup</h2>
        <p>Connect to LEFT and RIGHT monitors</p>
    </div>
</div>
```

**Step 2: Keep 2A (LEFT Monitor) unchanged**

Leave connection 2A as-is

**Step 3: Delete 2B (CENTER Monitor with HDMI Switch)**

Delete the entire 2B connection guide section including HDMI switch warning

**Step 4: Relabel 2C to 2B**

Change 2C header to 2B:

```html
<div class="connection-header work">
    <div class="connection-number work">2B</div>
    <div class="connection-info">
        <h4>Work Mac → RIGHT Monitor</h4>
        <p>Same pattern as Personal Mac</p>
    </div>
</div>
```

**Step 5: Verify Work Mac section**

Check that only 2A (LEFT) and 2B (RIGHT) exist

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update Work Mac section to 2 monitors, remove HDMI switch"
```

---

## Task 6: Update HP Dock Section - Remove CENTER (3B)

**Files:**
- Modify: `index.html:480-530`

**Step 1: Update section header**

Change section header subtitle:

```html
<div class="section-header hp">
    <div class="section-number hp">3</div>
    <div class="section-title">
        <h2>HP Dock Setup</h2>
        <p>Connect to LEFT and RIGHT monitors</p>
    </div>
</div>
```

**Step 2: Keep 3A (LEFT Monitor) unchanged**

Leave connection 3A as-is

**Step 3: Delete 3B (CENTER Monitor with HDMI Switch)**

Delete the entire 3B connection section including switch toggle warning

**Step 4: Relabel 3C to 3B**

Change 3C header to 3B:

```html
<div class="connection-header hp">
    <div class="connection-number hp">3B</div>
    <div class="connection-info">
        <h4>HP Dock → RIGHT Monitor</h4>
        <p>VGA connection</p>
    </div>
</div>
```

**Step 5: Verify HP Dock section**

Check that only 3A (LEFT) and 3B (RIGHT) exist

**Step 6: Commit**

```bash
git add index.html
git commit -m "docs: update HP Dock section to 2 monitors"
```

---

## Task 7: Update Software Configuration Section

**Files:**
- Modify: `index.html:540-590` (approximate)

**Step 1: Update Lunar configuration text**

Find and update all references to "all 3 monitors" → "both monitors":

```html
<div class="description"><strong>What it does:</strong> Verify all 2 monitors appear in Lunar menu bar icon</div>
```

**Step 2: Update hotkey descriptions**

Update Cmd+1/2/3 descriptions from "All 3 monitors" to "Both monitors":

```html
<tr><td>Cmd+1</td><td>Switch to Personal Mac</td><td>Both monitors</td></tr>
<tr><td>Cmd+2</td><td>Switch to Work Mac</td><td>Both monitors</td></tr>
<tr><td>Cmd+3</td><td>Switch to HP Dock</td><td>Both monitors</td></tr>
```

**Step 3: Remove HDMI switch references**

Update the help text to remove HDMI switch mention:

```html
<p style="margin-top: 15px; font-size: 0.9rem; color: #aaa;">
    Barrier: Move mouse to edge to switch computers | Lunar: Cmd+1/2/3 for monitor switching
</p>
```

**Step 4: Verify software section**

Check that all monitor counts and HDMI switch references are updated

**Step 5: Commit**

```bash
git add index.html
git commit -m "docs: update software config section for 2 monitors"
```

---

## Task 8: Update Wizard Completion Screen

**Files:**
- Modify: `index.html:715-742`

**Step 1: Update completion count**

Change "All 13 Steps Complete!" to "All 9 Steps Complete!" (line ~717):

```html
<h2>All 9 Steps Complete!</h2>
```

**Step 2: Update completion message**

Change message from "all 3 monitors" to "both monitors" (line ~718):

```html
<p>Congratulations! You've successfully connected all 3 computers to both monitors AND configured the software. Your KVM setup is now ready to use!</p>
```

**Step 3: Update hardware summary table**

Remove CENTER column from summary table (lines ~722-728):

```html
<table class="summary-table">
    <thead><tr><th>Computer</th><th>LEFT</th><th>RIGHT</th></tr></thead>
    <tbody>
        <tr><td>🟢 Personal</td><td>Hub→BENFEI→DP</td><td>USB-C→BENFEI→DP</td></tr>
        <tr><td>🟠 Work</td><td>Hub→BENFEI→DP</td><td>USB-C→BENFEI→DP</td></tr>
        <tr><td>🟣 HP Dock</td><td>DP→VGA</td><td>DP→VGA</td></tr>
    </tbody>
</table>
```

**Step 4: Update software summary**

Update hotkey table notes from "All 3 monitors" to "Both monitors" (lines ~732-736):

```html
<tbody>
    <tr><td>Cmd+1</td><td>Switch to Personal Mac</td><td>Both monitors</td></tr>
    <tr><td>Cmd+2</td><td>Switch to Work Mac</td><td>Both monitors</td></tr>
    <tr><td>Cmd+3</td><td>Switch to HP Dock</td><td>Both monitors</td></tr>
</tbody>
```

**Step 5: Update footer help text**

Remove HDMI switch reference (line ~738):

```html
<p style="margin-top: 15px; font-size: 0.9rem; color: #aaa;">
    Barrier: Move mouse to edge to switch computers | Lunar: Cmd+1/2/3 for monitor switching
</p>
```

**Step 6: Verify completion screen**

Check that table has 2 columns and all counts are updated

**Step 7: Commit**

```bash
git add index.html
git commit -m "docs: update wizard completion screen for 2 monitors"
```

---

## Task 9: Update JavaScript Wizard Data - Personal Mac

**Files:**
- Modify: `index.html:760-845`

**Step 1: Keep step 1a (LEFT) unchanged**

Leave the first step object as-is (lines ~764-793)

**Step 2: Delete step 1b (CENTER) completely**

Delete the entire step object for id '1b' (lines ~794-815):

```javascript
// DELETE THIS ENTIRE OBJECT
{
    id: '1b',
    title: 'CENTER Monitor',
    ...
},
```

**Step 3: Update step 1c id and title**

Change id from '1c' to '1b' and keep title as 'RIGHT Monitor' (line ~817):

```javascript
{
    id: '1b',  // Changed from '1c'
    title: 'RIGHT Monitor',
    subtitle: 'Similar to LEFT setup',
    // ... rest unchanged
}
```

**Step 4: Verify personal array**

Confirm personal.steps array has exactly 2 objects with ids '1a' and '1b'

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update wizard data for Personal Mac - 2 monitors"
```

---

## Task 10: Update JavaScript Wizard Data - Work Mac

**Files:**
- Modify: `index.html:847-935`

**Step 1: Keep step 2a (LEFT) unchanged**

Leave the first step object as-is

**Step 2: Delete step 2b (CENTER with HDMI Switch) completely**

Delete the entire step object for id '2b' including HDMI switch equipment and warning:

```javascript
// DELETE THIS ENTIRE OBJECT
{
    id: '2b',
    title: 'CENTER Monitor',
    subtitle: '🔀 Via HDMI Switch!',
    ...
    warning: { title: 'HDMI Switch Explained', ... }
},
```

**Step 3: Update step 2c to 2b**

Change id from '2c' to '2b':

```javascript
{
    id: '2b',  // Changed from '2c'
    title: 'RIGHT Monitor',
    subtitle: 'Similar to LEFT setup',
    // ... rest unchanged
}
```

**Step 4: Verify work array**

Confirm work.steps array has exactly 2 objects with ids '2a' and '2b'

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update wizard data for Work Mac - 2 monitors"
```

---

## Task 11: Update JavaScript Wizard Data - HP Dock

**Files:**
- Modify: `index.html:937-995`

**Step 1: Keep step 3a (LEFT) unchanged**

Leave the first step object as-is

**Step 2: Delete step 3b (CENTER with Switch) completely**

Delete the entire step object for id '3b':

```javascript
// DELETE THIS ENTIRE OBJECT
{
    id: '3b',
    title: 'CENTER Monitor',
    ...
    warning: { title: 'Switch Toggle Reminder', ... }
},
```

**Step 3: Update step 3c to 3b**

Change id from '3c' to '3b':

```javascript
{
    id: '3b',  // Changed from '3c'
    title: 'RIGHT Monitor',
    subtitle: 'VGA connection',
    // ... rest unchanged
}
```

**Step 4: Verify hp array**

Confirm hp.steps array has exactly 2 objects with ids '3a' and '3b'

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update wizard data for HP Dock - 2 monitors"
```

---

## Task 12: Update JavaScript Wizard Data - Software Steps

**Files:**
- Modify: `index.html:997-1090` (approximate)

**Step 1: Update Lunar verification step**

Find the Lunar verification step and update monitor count references:

```javascript
{
    id: 'software-1',
    title: 'Install Lunar',
    // ...
    detailedSteps: [
        // ...
        { text: 'Verify all 2 monitors appear in Lunar menu bar icon', tip: 'If missing, check BENFEI USB power and cables' }
    ],
    // ...
}
```

**Step 2: Update hotkey configuration step**

Update the hotkey setup instructions to reference 2 monitors:

```javascript
detailedSteps: [
    // ...
    { text: 'Set Cmd+1 to switch both monitors to Personal Mac inputs (DP/DP)', tip: 'Maps to: LEFT=DP, RIGHT=DP' },
    { text: 'Set Cmd+2 to switch both monitors to Work Mac inputs (DP/DP)', tip: 'Both via direct DP or adapters' },
    { text: 'Set Cmd+3 to switch both monitors to HP Dock inputs (VGA/VGA)', tip: 'Both via VGA adapters' },
    { text: 'Test each hotkey to verify switching works', tip: 'Press Cmd+1/2/3 and watch monitors change' }
]
```

**Step 3: Update final test step**

Update test step to reference 2 monitors:

```javascript
detailedSteps: [
    { text: 'Press Cmd+1 - Both monitors should switch to Personal Mac', tip: 'If not working, check Lunar permissions and DDC/CI' },
    { text: 'Press Cmd+2 - Both monitors should switch to Work Mac', tip: 'Check DP connections' },
    // ...
]
```

**Step 4: Verify software section**

Confirm all "3 monitors" changed to "2 monitors" or "both monitors"

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update wizard software steps for 2 monitors"
```

---

## Task 13: Test Wizard Progress Calculation

**Files:**
- Modify: `index.html` (JavaScript section with progress tracking functions)

**Step 1: Find and review progress calculation**

Search for functions that calculate total steps or progress percentage. Look for code like:

```javascript
// Find code similar to this
const totalSteps = wizardData.personal.steps.length +
                   wizardData.work.steps.length +
                   wizardData.hp.steps.length +
                   wizardData.software.steps.length;
```

**Step 2: Verify automatic calculation**

Since we've updated the arrays to have 2 steps each (personal, work, hp), the calculation should automatically show:
- Hardware: 6 steps (2 per computer × 3 computers)
- Software: ~3 steps
- Total: ~9 steps

No code changes should be needed if using `.length` properties.

**Step 3: Open index.html in browser**

Test the wizard and verify:
- Progress bar shows correct percentage
- Step counts are accurate
- "All 9 Steps Complete!" appears at end

**Step 4: Commit (only if changes needed)**

```bash
# Only if manual updates were required
git add index.html
git commit -m "fix: update wizard progress calculation for 9 total steps"
```

---

## Task 14: Deploy to Vercel

**Files:**
- Modify: `public/index.html` (copy file to deployment directory)

**Step 1: Copy updated file to public directory**

```bash
cp index.html public/index.html
```

**Step 2: Verify file in public directory**

```bash
ls -lh public/index.html
```

Expected: File exists and is recent

**Step 3: Test locally**

Open `public/index.html` in browser and:
- Check header says "2 Monitors"
- Navigate through full guide - verify no CENTER references
- Run through wizard - verify 9 steps total
- Check completion screen shows 2-column table

**Step 4: Commit deployment file**

```bash
git add public/index.html
git commit -m "deploy: update guide for 2-monitor setup"
```

**Step 5: Deploy to Vercel**

```bash
vercel --prod
```

Expected: Deployment succeeds, returns production URL

**Step 6: Verify live site**

Visit https://vercel-kvm.vercel.app/ and verify:
- Header shows "2 Monitors"
- Both tabs work (Full Guide + Wizard)
- No CENTER monitor references
- Wizard completes with 9 steps

---

## Task 15: Final Verification & Documentation

**Files:**
- Create: `CHANGELOG.md`
- Modify: `README.md` (if exists) or create it

**Step 1: Create CHANGELOG**

```markdown
# Changelog

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
```

**Step 2: Update or create README**

```markdown
# KVM Setup Guide

Complete visual guide for connecting 3 computers to 2 monitors with KVM functionality.

## Current Setup
- **Monitors:** 2x Samsung ViewFinity S65UC 34" (LS34C650UANXGO)
- **Computers:** Personal Mac, Work Mac, HP Dock
- **Features:** DDC/CI switching via Lunar, Barrier for unified mouse/keyboard

## Deployment
- Live site: https://vercel-kvm.vercel.app/
- Deployed via Vercel
- Updates: Push to main branch or `vercel --prod`

## Development
- Single-file HTML application
- No build process required
- Edit `index.html` and copy to `public/` for deployment
```

**Step 3: Commit documentation**

```bash
git add CHANGELOG.md README.md
git commit -m "docs: add changelog and README for v2.0.0"
```

**Step 4: Create git tag**

```bash
git tag -a v2.0.0 -m "Version 2.0.0: 2-monitor update with Samsung ViewFinity S65UC"
git push origin v2.0.0
```

**Step 5: Final verification checklist**

Create a test checklist and verify each item:

- [ ] Header shows "2 Monitors"
- [ ] TOC references LEFT and RIGHT only
- [ ] Equipment section has no HDMI switch
- [ ] Personal Mac has connections 1A (LEFT) and 1B (RIGHT)
- [ ] Work Mac has connections 2A (LEFT) and 2B (RIGHT)
- [ ] HP Dock has connections 3A (LEFT) and 3B (RIGHT)
- [ ] No "CENTER" references anywhere
- [ ] Wizard shows 9 total steps
- [ ] Wizard progress tracking works correctly
- [ ] Completion screen shows 2-column table
- [ ] Software section references "both monitors"
- [ ] No HDMI switch references
- [ ] Live site deployed and working

---

## Execution Notes

- Total estimated time: 90-120 minutes
- Can be done in single session
- Test in browser after each major section update
- Use browser dev tools to check for console errors
- Recommended browser: Chrome/Firefox for testing

## Rollback Plan

If issues occur:
```bash
git log --oneline  # Find commit before changes
git revert <commit-hash>
vercel --prod  # Redeploy previous version
```
