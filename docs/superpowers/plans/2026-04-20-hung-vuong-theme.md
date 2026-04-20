# Hung Vuong Theme UI Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign the badminton calculator UI with a Gio To Hung Vuong (10/3) theme — red/gold color scheme, wood/paper textures, traditional ornaments, and CSS animations — while keeping all JS logic and features unchanged.

**Architecture:** Single-file HTML app. All changes are CSS-only (swap variables, rewrite styles) plus adding SVG inline elements and CSS animation divs to the HTML body. No new files, no new JS libraries.

**Tech Stack:** Vanilla HTML/CSS, inline SVG, CSS animations, Google Fonts (Pangolin + Roboto — already loaded).

**Spec:** `docs/superpowers/specs/2026-04-20-hung-vuong-theme-design.md`

**File:** All changes in `index.html` (the only application file).

---

### Task 1: CSS Variables & Body Background (Wood Texture)

Replace the existing CSS custom properties and body background with the Hung Vuong theme palette and wood texture.

**Files:**
- Modify: `index.html:12-24` (`:root` variables)
- Modify: `index.html:27-35` (body styles)
- Modify: `index.html:36-39` (overlay)

- [ ] **Step 1: Replace `:root` CSS variables**

Replace the existing `:root` block (lines 12-24) with:

```css
:root {
    --primary: #8B0000;
    --primary-light: #C41E3A;
    --gold: #D4A017;
    --gold-light: #F0D060;
    --brown: #5D3A1A;
    --cream: #FFF8E7;
    --cream-dark: #F5E6C8;
    --male: #0984e3;
    --female: #e84393;
}
```

- [ ] **Step 2: Replace body background with CSS wood texture**

Replace the body styles (lines 27-35) with:

```css
body {
    font-family: 'Roboto', -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
    background:
        repeating-linear-gradient(
            90deg,
            transparent,
            rgba(0,0,0,0.03) 1px,
            transparent 2px,
            transparent 4px
        ),
        repeating-linear-gradient(
            0deg,
            rgba(74, 46, 20, 0.15) 0px,
            rgba(93, 58, 26, 0.1) 2px,
            rgba(62, 36, 16, 0.15) 4px
        ),
        linear-gradient(
            180deg,
            #5D3A1A 0%,
            #4A2E14 25%,
            #3E2410 50%,
            #4A2E14 75%,
            #5D3A1A 100%
        );
    display: flex; justify-content: center; align-items: center;
    min-height: 100vh; margin: 0; color: #333; padding: 15px; box-sizing: border-box;
    font-weight: 400;
}
```

- [ ] **Step 3: Update overlay to warm tone**

Replace the overlay styles (lines 36-39) with:

```css
.overlay {
    position: fixed; top: 0; left: 0; width: 100%; height: 100%;
    background: rgba(62, 36, 16, 0.2); z-index: 0; pointer-events: none;
}
```

- [ ] **Step 4: Open in browser and verify**

Open `index.html` in a browser. Expected: wood-toned brown background with grain texture, warm overlay. The card and content will look broken (wrong colors) — that's expected, we fix it in the next tasks.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: replace color palette and body background with Hung Vuong wood theme"
```

---

### Task 2: Container Card (Paper Texture) & Header/Title

Restyle the main container card to look like giay do (traditional Vietnamese paper) and update the header/title styling.

**Files:**
- Modify: `index.html` — `.container` styles (lines 42-50)
- Modify: `index.html` — `h2` and `.subtitle` styles (lines 53-64)
- Modify: `index.html` — HTML at line 179 (add banner + SVG ornaments before `<h2>`)

- [ ] **Step 1: Replace `.container` styles**

Replace the `.container` block (lines 42-50) with:

```css
.container {
    position: relative; z-index: 1;
    background:
        radial-gradient(ellipse at 20% 50%, rgba(245, 230, 200, 0.4) 0%, transparent 70%),
        radial-gradient(ellipse at 80% 30%, rgba(245, 230, 200, 0.3) 0%, transparent 60%),
        linear-gradient(180deg, var(--cream) 0%, #FFF5DC 100%);
    padding: 0 20px 20px 20px;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(93, 58, 26, 0.3);
    width: 100%; max-width: 450px;
    border: 2px solid var(--gold);
    overflow: hidden;
}
```

- [ ] **Step 2: Replace `h2` and `.subtitle` styles**

Replace h2 and subtitle styles (lines 53-64) with:

```css
h2 {
    font-family: 'Pangolin', cursive;
    margin-top: 0; font-weight: 800;
    color: var(--gold);
    font-size: 1.8rem; text-transform: uppercase; text-align: center;
    text-shadow: 0 0 10px rgba(212, 160, 23, 0.3);
    margin-bottom: 5px;
    background: linear-gradient(135deg, var(--primary), #6B1010);
    padding: 15px 20px 10px;
    margin-left: -20px; margin-right: -20px;
    border-radius: 0;
}
.subtitle {
    text-align: center; font-size: 0.9rem; color: var(--brown);
    margin-bottom: 20px; font-style: italic; font-weight: 400;
    background: linear-gradient(135deg, var(--primary), #6B1010);
    color: var(--cream-dark);
    padding: 0 20px 12px;
    margin-left: -20px; margin-right: -20px;
    margin-top: 0;
}
```

- [ ] **Step 3: Add banner HTML before `<h2>`**

Find line 179 (`<h2>🧧 CLB ĐỐT TIỀN CẦU 🧧</h2>`) and insert a banner div BEFORE it. Also replace the h2 content and add a Dong Son divider after subtitle:

Replace:
```html
    <h2>🧧 CLB ĐỐT TIỀN CẦU 🧧</h2>
    <div class="subtitle">Sân kinh tế, tính tiền đừng thắc mắc</div>
```

With:
```html
    <!-- Banner Mung Le -->
    <div class="hung-vuong-banner">
        <svg class="banner-cloud-left" width="30" height="15" viewBox="0 0 30 15"><path d="M0,15 Q5,5 10,10 Q15,0 20,8 Q25,2 30,12" fill="none" stroke="currentColor" stroke-width="1.5"/></svg>
        <span>✿ Mừng Giỗ Tổ Hùng Vương 10/3 ✿</span>
        <svg class="banner-cloud-right" width="30" height="15" viewBox="0 0 30 15"><path d="M0,12 Q5,2 10,8 Q15,0 20,10 Q25,5 30,15" fill="none" stroke="currentColor" stroke-width="1.5"/></svg>
    </div>

    <h2>
        <svg class="title-dragon" width="24" height="20" viewBox="0 0 24 20"><path d="M2,18 Q4,8 8,10 Q10,4 14,8 Q16,2 20,6 Q22,4 23,2" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/><circle cx="22" cy="3" r="1.5" fill="currentColor"/></svg>
        🏛️ CLB ĐỐT TIỀN CẦU 🏛️
        <svg class="title-dragon" width="24" height="20" viewBox="0 0 24 20" style="transform: scaleX(-1)"><path d="M2,18 Q4,8 8,10 Q10,4 14,8 Q16,2 20,6 Q22,4 23,2" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/><circle cx="22" cy="3" r="1.5" fill="currentColor"/></svg>
    </h2>
    <div class="subtitle">Sân kinh tế, tính tiền đừng thắc mắc</div>

    <!-- Dong Son Divider -->
    <div class="dongson-divider">
        <svg width="100%" height="20" viewBox="0 0 400 20" preserveAspectRatio="none">
            <defs>
                <pattern id="dongson" x="0" y="0" width="40" height="20" patternUnits="userSpaceOnUse">
                    <circle cx="20" cy="10" r="6" fill="none" stroke="var(--gold)" stroke-width="1"/>
                    <circle cx="20" cy="10" r="3" fill="none" stroke="var(--gold)" stroke-width="0.8"/>
                    <line x1="20" y1="0" x2="20" y2="4" stroke="var(--gold)" stroke-width="1"/>
                    <line x1="20" y1="16" x2="20" y2="20" stroke="var(--gold)" stroke-width="1"/>
                    <line x1="0" y1="10" x2="14" y2="10" stroke="var(--gold)" stroke-width="0.5"/>
                    <line x1="26" y1="10" x2="40" y2="10" stroke="var(--gold)" stroke-width="0.5"/>
                </pattern>
            </defs>
            <rect width="400" height="20" fill="url(#dongson)"/>
        </svg>
    </div>

    <!-- Lotus between banner and content -->
    <div class="lotus-icon">
        <svg width="30" height="28" viewBox="0 0 30 28">
            <path d="M15,4 Q13,12 9,20 Q15,17 15,17 Q15,17 21,20 Q17,12 15,4Z" fill="var(--primary)"/>
            <path d="M8,8 Q6,14 5,20 Q10,16 12,14" fill="var(--primary-light)" opacity="0.6"/>
            <path d="M22,8 Q24,14 25,20 Q20,16 18,14" fill="var(--primary-light)" opacity="0.6"/>
            <circle cx="15" cy="13" r="2.5" fill="var(--gold)"/>
        </svg>
    </div>
```

- [ ] **Step 4: Add CSS for new banner elements**

Add these styles BEFORE the `/* Section Title */` comment (before line 67):

```css
/* Banner Mung Le */
.hung-vuong-banner {
    background: linear-gradient(135deg, var(--primary), #6B0000);
    color: var(--gold);
    text-align: center;
    padding: 8px 16px;
    font-family: 'Pangolin', cursive;
    font-size: 14px;
    font-weight: 700;
    border-radius: 12px 12px 0 0;
    margin: -0px -20px 0 -20px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    border-bottom: 1px solid var(--gold);
}
.banner-cloud-left, .banner-cloud-right { color: var(--gold); flex-shrink: 0; }
.title-dragon { color: var(--gold); vertical-align: middle; }

/* Dong Son Divider */
.dongson-divider {
    margin: 0 -20px 10px;
    opacity: 0.6;
    line-height: 0;
}

/* Lotus Icon */
.lotus-icon {
    text-align: center;
    margin: -5px 0 10px;
}
```

- [ ] **Step 5: Open in browser and verify**

Expected: paper-textured card with gold border, red banner at top with "Mung Gio To Hung Vuong 10/3", gold title text on red background, Dong Son pattern divider, lotus icon.

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: add paper-textured card, banner, header ornaments and Dong Son divider"
```

---

### Task 3: Section Titles, Inputs, Buttons & Toggles

Restyle all form elements to match the Hung Vuong theme.

**Files:**
- Modify: `index.html` — `.section-title` styles (lines 67-75)
- Modify: `index.html` — input/label styles (lines 78-90)
- Modify: `index.html` — button styles (lines 93-103)
- Modify: `index.html` — bank-config, switch styles (lines 112-118)
- Modify: `index.html` — result styles (lines 106-109)
- Modify: `index.html` — HTML section-title emoji replacement (line 249)

- [ ] **Step 1: Replace `.section-title` styles**

Replace the `.section-title` block with:

```css
.section-title {
    font-size: 0.8rem; color: var(--gold);
    background: linear-gradient(135deg, var(--primary), #6B1010);
    padding: 6px 12px; border-radius: 15px;
    display: inline-block; margin-top: 10px; margin-bottom: 8px;
    font-weight: 700; text-transform: uppercase;
    border: 1px solid var(--gold);
    box-shadow: 0 2px 4px rgba(93, 58, 26, 0.18);
}
```

- [ ] **Step 2: Replace input/label styles**

Replace label and input styles (lines 80-90) with:

```css
label { display: block; margin-bottom: 5px; font-size: 0.85rem; font-weight: 600; color: var(--primary); }
input, select {
    width: 100%; padding: 10px;
    border: 1px solid var(--gold);
    border-radius: 8px; font-size: 16px;
    background: var(--cream); font-weight: 500;
    color: var(--brown);
    appearance: none; box-sizing: border-box;
}
input:focus, select:focus { outline: none; border-color: var(--gold-light); box-shadow: 0 0 8px rgba(212, 160, 23, 0.4); }
#tienCau { border-color: var(--primary); color: var(--primary); font-weight: 700; background: #FFF0E0; }
```

- [ ] **Step 3: Replace button styles**

Replace button styles (lines 94-103) with:

```css
button {
    padding: 12px; border: none; border-radius: 10px;
    font-size: 15px; font-weight: 700; cursor: pointer;
    transition: 0.2s; text-transform: uppercase; flex: 1; color: var(--gold);
    border: 1px solid var(--gold);
}
.btn-calc { background: linear-gradient(135deg, var(--primary), #6B1010); box-shadow: 0 3px 0 #4A0000; }
.btn-calc:hover { box-shadow: 0 3px 12px rgba(212, 160, 23, 0.4); }
.btn-calc:active { transform: translateY(3px); box-shadow: none; }
.btn-camera { background: linear-gradient(135deg, var(--gold), #B8860B); color: var(--primary); box-shadow: 0 3px 0 #8B6914; display: none; }
.btn-camera:active { transform: translateY(3px); box-shadow: none; }
```

- [ ] **Step 4: Replace bank-config and switch styles**

Replace bank-config and switch styles (lines 112-118) with:

```css
.bank-config { background: rgba(255, 248, 231, 0.6); padding: 15px; border-radius: 12px; border: 1px solid var(--gold); margin-bottom: 15px; }
.switch-toggle { display: flex; background: var(--cream-dark); border-radius: 20px; padding: 3px; margin: 10px 0; }
.switch-btn { flex: 1; text-align: center; padding: 8px; border-radius: 17px; cursor: pointer; font-size: 0.85rem; font-weight: 600; color: var(--brown); transition: 0.3s; }
.switch-btn.active { background: linear-gradient(135deg, var(--primary), #6B1010); color: var(--gold); box-shadow: 0 2px 5px rgba(93, 58, 26, 0.18); }
```

- [ ] **Step 5: Replace result and divider styles**

Replace result styles (lines 106-109) with:

```css
.result { margin-top: 20px; padding: 15px; background: rgba(255, 255, 255, 0.7); border-radius: 12px; border: 2px dashed var(--gold); display: none; }
.result-item { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 1rem; font-weight: 400; color: var(--brown); }
.result-item span:last-child { font-weight: 700; }
.divider { height: 1px; background: var(--gold); opacity: 0.3; margin: 12px 0; }
```

- [ ] **Step 6: Replace file-upload and misc color references**

Replace file-upload-wrapper styles (line 116) with:

```css
.file-upload-wrapper { border: 2px dashed var(--gold); border-radius: 10px; height: 80px; display: flex; flex-direction: column; justify-content: center; align-items: center; position: relative; color: var(--brown); background: white; cursor: pointer;}
.file-upload-wrapper input { position: absolute; width: 100%; height: 100%; opacity: 0; cursor: pointer; }
.upload-success-text { color: var(--primary); font-weight: 700; display: none; margin-top: 5px; font-size: 0.8rem; }
```

- [ ] **Step 7: Replace 🔥 emoji with 🏛️ in HTML**

In line 249, replace:
```html
<div class="section-title" style="background: linear-gradient(135deg, #246f92, var(--cyan-500));">🔥 Thiệt Hại Lông Lá</div>
```
With:
```html
<div class="section-title">🏛️ Thiệt Hại Lông Lá</div>
```

Also remove the inline `style` override on the attendance section-title (line 256):
```html
<div class="section-title" style="background: linear-gradient(135deg, var(--success-700), var(--success-600));">👽 Điểm Danh</div>
```
Replace with:
```html
<div class="section-title">👽 Điểm Danh</div>
```

- [ ] **Step 8: Update inline color references in HTML**

Find all inline `style` attributes referencing old color variables and update them:

- Line 222: `color: var(--slate-700)` → `color: var(--brown)`
- Line 253: `color: var(--slate-700)` → `color: var(--brown)`
- Line 268: `color:var(--navy-800)` → `color:var(--primary)`
- Line 274: `color: var(--navy-800)` → `color: var(--primary)`

- [ ] **Step 9: Open in browser and verify**

Expected: all form elements use red/gold theme. Section titles are red with gold text. Inputs have gold borders and cream background. Buttons are red with gold text.

- [ ] **Step 10: Commit**

```bash
git add index.html
git commit -m "feat: restyle form elements, buttons, and toggles with Hung Vuong theme"
```

---

### Task 4: Corner Cloud Ornaments

Add decorative SVG cloud ornaments to the 4 corners of the main container card.

**Files:**
- Modify: `index.html` — add SVG elements inside `.container` (after line 178, right after `<div class="container">`)
- Modify: `index.html` — add CSS for corner clouds

- [ ] **Step 1: Add corner cloud SVGs inside `.container`**

Right after `<div class="container">` (line 178), add:

```html
    <!-- Corner Cloud Ornaments -->
    <svg class="corner-cloud corner-tl" width="40" height="40" viewBox="0 0 40 40"><path d="M0,0 Q10,8 8,15 Q15,12 20,18 Q18,8 25,5 Q15,2 10,0Z" fill="var(--gold)" opacity="0.2"/></svg>
    <svg class="corner-cloud corner-tr" width="40" height="40" viewBox="0 0 40 40"><path d="M40,0 Q30,8 32,15 Q25,12 20,18 Q22,8 15,5 Q25,2 30,0Z" fill="var(--gold)" opacity="0.2"/></svg>
    <svg class="corner-cloud corner-bl" width="40" height="40" viewBox="0 0 40 40"><path d="M0,40 Q10,32 8,25 Q15,28 20,22 Q18,32 25,35 Q15,38 10,40Z" fill="var(--gold)" opacity="0.2"/></svg>
    <svg class="corner-cloud corner-br" width="40" height="40" viewBox="0 0 40 40"><path d="M40,40 Q30,32 32,25 Q25,28 20,22 Q22,32 15,35 Q25,38 30,40Z" fill="var(--gold)" opacity="0.2"/></svg>
```

- [ ] **Step 2: Add CSS for corner clouds**

Add after the `.lotus-icon` styles:

```css
/* Corner Cloud Ornaments */
.corner-cloud { position: absolute; pointer-events: none; z-index: 0; }
.corner-tl { top: 0; left: 0; }
.corner-tr { top: 0; right: 0; }
.corner-bl { bottom: 0; left: 0; }
.corner-br { bottom: 0; right: 0; }
```

- [ ] **Step 3: Open in browser and verify**

Expected: subtle gold cloud ornaments visible in each corner of the card, semi-transparent.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add decorative corner cloud ornaments to container"
```

---

### Task 5: Wave Dividers Between Sections

Add SVG wave/cloud dividers between form sections for visual separation.

**Files:**
- Modify: `index.html` — add SVG divider elements between sections in HTML
- Modify: `index.html` — add CSS for wave dividers

- [ ] **Step 1: Add CSS for wave divider**

Add after corner cloud styles:

```css
/* Wave Divider */
.wave-divider {
    margin: 5px -20px;
    opacity: 0.4;
    line-height: 0;
    text-align: center;
}
```

- [ ] **Step 2: Add wave dividers in HTML between form sections**

After the closing `</div>` of `.bank-config` (line 238) and before the "Chi Phi Mat Bang" section-title (line 240), add:

```html
    <div class="wave-divider">
        <svg width="100%" height="10" viewBox="0 0 400 10" preserveAspectRatio="none">
            <path d="M0,5 Q25,0 50,5 Q75,10 100,5 Q125,0 150,5 Q175,10 200,5 Q225,0 250,5 Q275,10 300,5 Q325,0 350,5 Q375,10 400,5" fill="none" stroke="var(--gold)" stroke-width="1.5"/>
        </svg>
    </div>
```

Add the same wave divider HTML between each major section:
- After "Chi Phi Mat Bang" inputs (after line 248, before the "Thiet Hai Long La" section)
- After "Thiet Hai Long La" inputs (after line 254, before the "Diem Danh" section)

- [ ] **Step 3: Open in browser and verify**

Expected: subtle gold wave lines separating the form sections.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add wave dividers between form sections"
```

---

### Task 6: CSS Animations — Falling Lotus Petals

Add falling lotus petal animation elements.

**Files:**
- Modify: `index.html` — add petal divs right after `<body>` tag
- Modify: `index.html` — add CSS keyframes and petal styles

- [ ] **Step 1: Add petal HTML elements after `<body>`**

Right after `<body>` (line 165), add:

```html
<!-- Falling Lotus Petals -->
<div class="petal petal-1"></div>
<div class="petal petal-2"></div>
<div class="petal petal-3"></div>
<div class="petal petal-4"></div>
<div class="petal petal-5"></div>
<div class="petal petal-6"></div>
<div class="petal petal-7"></div>
<div class="petal petal-8"></div>
```

- [ ] **Step 2: Add petal CSS and keyframes**

Add at the end of the `<style>` block, before `</style>`:

```css
/* Falling Lotus Petals */
@keyframes petalFall {
    0% { transform: translateY(-20px) translateX(0) rotate(0deg); opacity: 0; }
    10% { opacity: 0.6; }
    50% { transform: translateY(50vh) translateX(30px) rotate(180deg); opacity: 0.4; }
    100% { transform: translateY(105vh) translateX(-20px) rotate(360deg); opacity: 0; }
}

.petal {
    position: fixed;
    width: 12px; height: 18px;
    background: rgba(200, 100, 120, 0.3);
    clip-path: ellipse(50% 50% at 50% 50%);
    border-radius: 50% 50% 50% 0;
    pointer-events: none;
    z-index: 0;
    animation: petalFall linear infinite;
    will-change: transform;
}
.petal-1 { left: 5%; animation-duration: 10s; animation-delay: 0s; width: 10px; height: 16px; }
.petal-2 { left: 15%; animation-duration: 13s; animation-delay: 2s; width: 14px; height: 20px; }
.petal-3 { left: 30%; animation-duration: 11s; animation-delay: 4s; }
.petal-4 { left: 45%; animation-duration: 14s; animation-delay: 1s; width: 10px; height: 15px; }
.petal-5 { left: 60%; animation-duration: 9s; animation-delay: 3s; width: 13px; height: 19px; }
.petal-6 { left: 75%; animation-duration: 12s; animation-delay: 5s; }
.petal-7 { left: 85%; animation-duration: 15s; animation-delay: 2.5s; width: 11px; height: 17px; }
.petal-8 { left: 95%; animation-duration: 10s; animation-delay: 6s; width: 9px; height: 14px; }
```

- [ ] **Step 3: Open in browser and verify**

Expected: semi-transparent pink petal shapes gently falling from top to bottom across the page. They should not block clicking on any form elements.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add falling lotus petal CSS animation"
```

---

### Task 7: CSS Animations — Incense Smoke

Add subtle rising smoke animation from the bottom.

**Files:**
- Modify: `index.html` — add smoke divs after petal divs
- Modify: `index.html` — add CSS keyframes and smoke styles

- [ ] **Step 1: Add smoke HTML elements after the petal divs**

After the last `<div class="petal petal-8"></div>`, add:

```html
<!-- Incense Smoke -->
<div class="smoke smoke-1"></div>
<div class="smoke smoke-2"></div>
<div class="smoke smoke-3"></div>
```

- [ ] **Step 2: Add smoke CSS and keyframes**

Add after the petal styles:

```css
/* Incense Smoke */
@keyframes smokeRise {
    0% { transform: translateY(0) scale(1); opacity: 0.08; }
    50% { transform: translateY(-40vh) scale(2); opacity: 0.04; }
    100% { transform: translateY(-80vh) scale(3.5); opacity: 0; }
}

.smoke {
    position: fixed;
    bottom: -20px;
    width: 80px; height: 80px;
    background: rgba(255, 255, 255, 0.08);
    border-radius: 50%;
    filter: blur(20px);
    pointer-events: none;
    z-index: 0;
    animation: smokeRise ease-out infinite;
    will-change: transform;
}
.smoke-1 { left: 10%; animation-duration: 15s; animation-delay: 0s; width: 60px; height: 60px; }
.smoke-2 { left: 50%; animation-duration: 20s; animation-delay: 5s; width: 100px; height: 100px; }
.smoke-3 { right: 10%; animation-duration: 18s; animation-delay: 8s; width: 70px; height: 70px; }
```

- [ ] **Step 3: Open in browser and verify**

Expected: very subtle, nearly invisible white smoke wisps rising from the bottom of the page. Barely noticeable unless you look carefully.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add incense smoke rising CSS animation"
```

---

### Task 8: Accessibility — Reduced Motion

Add prefers-reduced-motion media query to disable all animations for users who prefer reduced motion.

**Files:**
- Modify: `index.html` — add media query at end of `<style>`

- [ ] **Step 1: Add reduced motion media query**

Add at the very end of the `<style>` block, before `</style>`:

```css
/* Accessibility: disable animations for reduced motion preference */
@media (prefers-reduced-motion: reduce) {
    .petal, .smoke { animation: none; display: none; }
}
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add prefers-reduced-motion to disable animations for accessibility"
```

---

### Task 9: Invoice Restyling

Update the hidden invoice template to match the Hung Vuong theme.

**Files:**
- Modify: `index.html` — invoice CSS styles (lines 121-156)
- Modify: `index.html` — modal styles (lines 159-162)

- [ ] **Step 1: Replace invoice CSS styles**

Replace the `#invoice-node` styles (lines 125-128) with:

```css
#invoice-node {
    width: 100%; background: #fff; padding: 25px;
    font-family: 'Courier New', Courier, monospace;
    color: #000; border: 5px double var(--primary);
    position: relative; box-sizing: border-box;
}
```

Replace `.inv-title` (line 133):
```css
.inv-title { font-size: 1.5rem; font-weight: 700; color: var(--primary); font-family: 'Roboto', sans-serif; text-transform: uppercase; }
```

Replace `.inv-total` (line 136):
```css
.inv-total { border-top: 2px dashed var(--primary); margin-top: 10px; padding-top: 10px; font-weight: 700; font-size: 1.2rem; color: var(--primary); }
```

Replace `.stamp-box` (lines 145-155):
```css
.stamp-box {
    position: absolute; bottom: 70px; right: 30px;
    width: 90px; height: 90px; border-radius: 50%;
    border: 3px solid var(--primary);
    display: flex; flex-direction: column; justify-content: center; align-items: center;
    color: var(--primary); font-weight: 700; font-size: 0.8rem;
    text-transform: uppercase; text-align: center;
    transform: rotate(-20deg); opacity: 0.8; z-index: 10;
    pointer-events: none; background: rgba(255, 255, 255, 0.7);
    font-family: 'Roboto', sans-serif; line-height: 1.2;
}
.stamp-inner { border-top: 1px solid var(--primary); border-bottom: 1px solid var(--primary); padding: 2px 0; margin-top: 3px; font-size: 0.7rem; font-weight: 900; }
```

- [ ] **Step 2: Update modal button styles**

Replace `.modal-btn-close` (line 162):
```css
.modal-btn-close { margin-top: 20px; padding: 10px 30px; background: linear-gradient(135deg, var(--primary), #6B1010); color: var(--gold); border: none; border-radius: 20px; font-weight: 600; cursor: pointer; font-size: 16px; border: 2px solid var(--gold); }
```

- [ ] **Step 3: Update invoice loading text emoji in HTML**

In line 170, replace:
```html
<div style="color: white; font-size: 1.2rem; margin-bottom: 10px; font-weight: 500;" id="loadingText">🧧 Đang xuất hóa đơn...</div>
```
With:
```html
<div style="color: white; font-size: 1.2rem; margin-bottom: 10px; font-weight: 500;" id="loadingText">🏛️ Đang xuất hóa đơn...</div>
```

And in line 172, replace `var(--cyan-400)` with `var(--gold)`:
```html
<div style="color: var(--gold); margin-bottom: 5px; font-size: 0.9rem;">👇 Nhấn giữ ảnh để LƯU nhé!</div>
```

- [ ] **Step 4: Open in browser, trigger invoice capture and verify**

Expected: invoice border and stamp are red, title and totals are red, modal close button is red/gold.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: restyle invoice and modal with Hung Vuong red/gold theme"
```

---

### Task 10: Final Cleanup & Title Update

Update page title and clean up any remaining old color references.

**Files:**
- Modify: `index.html` — `<title>` tag (line 6)
- Modify: `index.html` — remaining inline old-variable references

- [ ] **Step 1: Update page title**

Replace line 6:
```html
<title> CLB Đốt Tiền Cầu - Phiên bản mùa hè </title>
```
With:
```html
<title>CLB Đốt Tiền Cầu - Mừng Giỗ Tổ Hùng Vương 🏛️</title>
```

- [ ] **Step 2: Search and replace remaining old variable references**

Search the entire file for any remaining references to old CSS variables (`--navy-`, `--cyan-`, `--slate-`, `--success-`, `--ice-`). For each found:
- `var(--navy-800)` or `var(--navy-900)` → `var(--primary)`
- `var(--navy-700)` → `var(--primary)`
- `var(--cyan-500)` or `var(--cyan-400)` → `var(--gold)`
- `var(--cyan-200)` → `var(--cream)`
- `var(--ice-100)` → `var(--cream)`
- `var(--slate-700)` or `var(--slate-900)` → `var(--brown)`
- `var(--success-600)` or `var(--success-700)` → `var(--primary)`
- `#b7dde5` → `var(--gold)`
- `#c7e8ee` → `var(--gold)` with opacity
- `#bfe6ee` → `var(--gold)`
- `#d7eef3` → `var(--cream-dark)`
- `#eef9fc` → `#FFF0E0`

Note: Leave `#0984e3` (male blue) and `#e84393` (female pink) unchanged — they are intentionally kept.

- [ ] **Step 3: Full visual test in browser**

Open `index.html` and test the complete flow:
1. Page loads with wood background, paper card, red/gold theme
2. Banner shows "Mung Gio To Hung Vuong 10/3"
3. Petals fall, smoke rises (subtle)
4. Corner clouds visible
5. Fill in form values and click "Bam Xem Ai Ngheo Hon"
6. Results show with gold dashed border
7. QR codes display with blue/pink borders
8. Click "Xuat Hoa Don" — invoice shows with red theme
9. All buttons, inputs, toggles use red/gold colors
10. No old blue/cyan colors visible anywhere

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: final cleanup — update title and replace all old color references"
```
