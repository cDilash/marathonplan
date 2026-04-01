# SF Marathon Training Plan Website — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-file cinematic vertical-scroll website presenting a 17-week SF Marathon training plan with Dark & Athletic visual theme, pure HTML/CSS.

**Architecture:** One `index.html` file containing all HTML structure with embedded `<style>` block. CSS custom properties for theming, CSS `animation-timeline` for scroll animations, `position: sticky` for navigation. Content organized as 12 sequential `<section>` elements. Google Fonts loaded via `<link>`.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, scroll-driven animations), Google Fonts (Inter, JetBrains Mono)

---

## File Structure

- **Create:** `index.html` — the entire website (single file, ~3000-4000 lines)

No other files needed. The spec lives at `docs/superpowers/specs/2026-03-31-sf-marathon-training-site-design.md`.

---

## Phase 1: Foundation

### Task 1: HTML Document Shell + CSS Theme System

**Files:**
- Create: `index.html`

This task creates the complete document skeleton with all CSS custom properties, typography, base styles, and empty section placeholders.

- [ ] **Step 1: Create index.html with full CSS theme**

Create `index.html` with:
- `<!DOCTYPE html>` declaration, meta viewport, charset
- Google Fonts `<link>` tags for Inter (400, 600, 700, 900) and JetBrains Mono (500)
- Full `<style>` block containing:
  - CSS custom properties (`:root`) for all 17 color tokens from the spec
  - CSS reset (`*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }`)
  - `html { scroll-behavior: smooth; }` and `body` base styles (background `var(--base)`, color `var(--text-secondary)`, font-family Inter)
  - Typography classes: `.phase-heading`, `.section-title`, `.week-heading`, `.body-text`, `.data-mono`, `.label`
  - Layout utilities: `.container` (max-width 900px, margin auto, padding 0 24px), `.section` (padding 120px 0)
  - Card styles: `.card` (background `var(--card)`, border-radius 12px, border 1px solid `var(--border)`, padding 24-32px)
  - Session type color classes: `.session-easy`, `.session-quality`, `.session-long`, `.session-rest`, `.session-strength`
  - Zone color classes: `.zone-2`, `.zone-3`, `.zone-4`, `.zone-5`
  - Badge styles: `.badge` (small pill), `.badge-stepback` (yellow/warning variant)
  - Sticky nav styles (see Task 2)
- 12 empty `<section>` elements with IDs: `hero`, `overview`, `phase-1`, `phase-2`, `phase-3`, `phase-4`, `course-map`, `race-day`, `hill-programming`, `strength`, `nutrition`, `risk-management`

- [ ] **Step 2: Open in browser to verify**

Run: `open index.html` (macOS) — verify dark background loads, no errors in console, all 12 sections exist as empty blocks.

- [ ] **Step 3: Commit**

```bash
git init
git add index.html
git commit -m "feat: HTML shell with full CSS theme system and 12 section placeholders"
```

---

### Task 2: Sticky Navigation Bar

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add sticky nav HTML**

Add immediately after `<body>` tag, before the first section:

```html
<nav class="sticky-nav">
  <div class="nav-inner">
    <div class="nav-title">SF MARATHON PLAN</div>
    <div class="nav-progress">
      <div class="nav-progress-bar"></div>
    </div>
    <div class="nav-countdown">118 DAYS</div>
  </div>
</nav>
```

- [ ] **Step 2: Add sticky nav CSS**

Add to `<style>` block:

```css
.sticky-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 48px;
  background: rgba(10, 10, 10, 0.9);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  z-index: 100;
  border-bottom: 1px solid var(--border);
}

.nav-inner {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 24px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-title {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 700;
  font-size: 12px;
  letter-spacing: 3px;
  color: var(--text-muted);
  text-transform: uppercase;
}

.nav-progress {
  flex: 1;
  max-width: 200px;
  height: 3px;
  background: var(--border);
  border-radius: 2px;
  margin: 0 24px;
  overflow: hidden;
}

.nav-progress-bar {
  height: 100%;
  width: 100%;
  background: var(--primary);
  border-radius: 2px;
  transform-origin: left;
  transform: scaleX(0);
  animation: progress-fill linear;
  animation-timeline: scroll();
}

@keyframes progress-fill {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}

.nav-countdown {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  font-size: 12px;
  color: var(--primary);
  letter-spacing: 1px;
}
```

- [ ] **Step 3: Verify in browser**

Open `index.html` — verify sticky nav is visible at top, progress bar animates as you scroll (Chrome/Edge), countdown shows "118 DAYS" in orange monospace.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: sticky navigation bar with CSS scroll progress"
```

---

### Task 3: Hero Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hero HTML**

Replace the empty `<section id="hero">` with:

```html
<section id="hero" class="hero">
  <div class="hero-bg"></div>
  <div class="hero-content">
    <div class="hero-label">July 27, 2026</div>
    <h1 class="hero-title">SAN FRANCISCO<br/>MARATHON</h1>
    <div class="hero-divider"></div>
    <p class="hero-subtitle">17-Week Training Plan</p>
    <div class="hero-stats">
      <div class="hero-stat">
        <span class="hero-stat-value">51.6</span>
        <span class="hero-stat-label">VO2max</span>
      </div>
      <div class="hero-stat-separator"></div>
      <div class="hero-stat">
        <span class="hero-stat-value">13</span>
        <span class="hero-stat-label">mi/wk current</span>
      </div>
      <div class="hero-stat-separator"></div>
      <div class="hero-stat">
        <span class="hero-stat-value">4:00</span>
        <span class="hero-stat-label">target finish</span>
      </div>
    </div>
    <div class="hero-countdown">
      <span class="hero-countdown-number">118</span>
      <span class="hero-countdown-label">days to race</span>
    </div>
    <div class="hero-scroll-indicator">
      <div class="hero-scroll-arrow"></div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add hero CSS**

```css
.hero {
  position: relative;
  height: 100vh;
  min-height: 700px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  padding-top: 48px;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 30% 20%, rgba(255, 106, 0, 0.08) 0%, transparent 60%),
    radial-gradient(ellipse at 70% 80%, rgba(255, 59, 48, 0.05) 0%, transparent 50%),
    linear-gradient(135deg, #0a0a0a 0%, #111118 50%, #0a0a0a 100%);
}

.hero-content {
  position: relative;
  text-align: center;
  z-index: 1;
}

.hero-label {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 600;
  font-size: 11px;
  letter-spacing: 6px;
  color: var(--text-muted);
  text-transform: uppercase;
  margin-bottom: 24px;
}

.hero-title {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 900;
  font-size: clamp(40px, 8vw, 80px);
  letter-spacing: -3px;
  line-height: 0.95;
  color: var(--text-primary);
  text-transform: uppercase;
}

.hero-divider {
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, var(--primary), var(--danger));
  margin: 32px auto;
  border-radius: 2px;
}

.hero-subtitle {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 400;
  font-size: 20px;
  color: var(--text-muted);
  letter-spacing: 2px;
}

.hero-stats {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 32px;
  margin-top: 48px;
}

.hero-stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.hero-stat-value {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  font-size: 28px;
  color: var(--primary);
}

.hero-stat-label {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 600;
  font-size: 10px;
  letter-spacing: 3px;
  color: var(--text-dim);
  text-transform: uppercase;
}

.hero-stat-separator {
  width: 1px;
  height: 40px;
  background: var(--border);
}

.hero-countdown {
  margin-top: 48px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.hero-countdown-number {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  font-size: 64px;
  color: var(--text-primary);
  animation: pulse 3s ease-in-out infinite;
}

.hero-countdown-label {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 600;
  font-size: 11px;
  letter-spacing: 4px;
  color: var(--text-dim);
  text-transform: uppercase;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}

.hero-scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
}

.hero-scroll-arrow {
  width: 20px;
  height: 20px;
  border-right: 2px solid var(--text-dim);
  border-bottom: 2px solid var(--text-dim);
  transform: rotate(45deg);
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% { transform: rotate(45deg) translate(0, 0); opacity: 0.5; }
  50% { transform: rotate(45deg) translate(5px, 5px); opacity: 1; }
}
```

- [ ] **Step 3: Verify in browser**

Open `index.html` — verify hero takes full viewport, title is massive and bold, stat pills show VO2max/mileage/target, countdown pulses, scroll arrow bounces, gradient background is subtle.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: hero section with race title, stats, countdown"
```

---

### Task 4: Overview / Periodization Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add overview HTML**

Replace the empty `<section id="overview">` with the full overview section containing:
- Section header "PERIODIZATION ARCHITECTURE"
- 4 phase summary cards in a grid (Base / Build / Peak / Taper), each with: phase name, week range, mileage range, runs/week, focus keywords
- Full periodization table matching the spec (Phase / Weeks / Focus / Weekly Mileage / Runs/Week / Strength)
- Goal calibration text block with the 4:00 primary and 3:45 stretch targets
- "Realistic assessment" paragraph about VO2max vs actual race fitness

The HTML should use `.container` for centering, `.section` for padding, `.card` for phase cards, and a styled `<table>` for the periodization table.

- [ ] **Step 2: Add overview-specific CSS**

Add CSS for:
- `.phase-cards` — grid layout, 4 columns on desktop, 2 on tablet, 1 on mobile
- `.phase-card` — styled card with left border accent color (orange for each phase)
- `.phase-card-number` — large phase number
- `.periodization-table` — styled table with `var(--card)` background, alternating row subtle shading, `var(--border)` cell borders
- `.goal-block` — callout block with left border accent for goal calibration text

- [ ] **Step 3: Verify in browser**

Scroll past hero — verify 4 phase cards render in a row, periodization table is readable with proper styling, goal text is clear.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: overview section with phase cards and periodization table"
```

---

### **CHECKPOINT: Phase 1 Complete**

Stop here. Open `index.html` in browser. User reviews:
- Sticky nav with scroll progress bar
- Full-viewport hero with race title, stats, countdown
- Overview section with 4 phase cards and periodization table
- Overall dark theme, typography, spacing

User confirms before proceeding to Phase 2.

---

## Phase 2: Training Weeks

### Task 5: Week Card CSS Component

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add week card CSS**

Add CSS for the reusable week card component that will be used 17 times:

```css
.week-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  margin-bottom: 32px;
  overflow: hidden;
}

.week-card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 24px;
  border-bottom: 1px solid var(--border);
}

.week-card-title {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 600;
  font-size: 20px;
  color: var(--text-primary);
}

.week-card-mileage {
  font-family: 'JetBrains Mono', monospace;
  font-weight: 500;
  font-size: 14px;
  color: var(--primary);
  background: rgba(255, 106, 0, 0.1);
  padding: 4px 12px;
  border-radius: 20px;
  border: 1px solid rgba(255, 106, 0, 0.2);
}

.week-card-focus {
  font-size: 13px;
  color: var(--text-muted);
  padding: 0 24px;
  margin-top: -4px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--border);
}

.badge-stepback {
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 700;
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--warning);
  background: rgba(255, 214, 10, 0.1);
  padding: 4px 10px;
  border-radius: 20px;
  border: 1px solid rgba(255, 214, 10, 0.2);
  margin-left: 12px;
}

.day-table {
  width: 100%;
  border-collapse: collapse;
}

.day-table tr {
  border-bottom: 1px solid var(--border);
}

.day-table tr:last-child {
  border-bottom: none;
}

.day-table td {
  padding: 12px 24px;
  font-size: 14px;
  vertical-align: top;
}

.day-table .day-name {
  width: 48px;
  font-family: 'Inter', system-ui, sans-serif;
  font-weight: 600;
  font-size: 12px;
  letter-spacing: 1px;
  color: var(--text-muted);
  text-transform: uppercase;
}

.day-table .day-session {
  font-weight: 600;
  color: var(--text-primary);
  min-width: 160px;
}

.day-table .day-details {
  color: var(--text-secondary);
  line-height: 1.6;
  font-size: 13px;
}

.day-table .day-details .treadmill {
  color: var(--text-muted);
  font-size: 12px;
  margin-top: 4px;
  font-style: italic;
}

/* Session type row accents */
.day-row-rest { opacity: 0.5; }
.day-row-easy td.day-session { color: var(--text-secondary); }
.day-row-quality td.day-session { color: var(--primary); }
.day-row-quality { border-left: 3px solid var(--primary); }
.day-row-long td.day-session { color: var(--primary); }
.day-row-long { border-left: 3px solid var(--primary); background: rgba(255, 106, 0, 0.03); }
.day-row-strength td.day-session { color: var(--text-muted); }
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: week card CSS component for training days"
```

---

### Task 6: Phase 1 — Base Building (Weeks 1-5)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Phase 1 section HTML**

Replace the empty `<section id="phase-1">` with the complete Phase 1 section containing:
- Phase header: "PHASE 1 — BASE" with "Weeks 1-5 · 15→22 mi/wk" subtitle
- Phase intro paragraphs (Z2 discipline focus, connective tissue adaptation, every run Zone 2 HR 116-136)
- Week 1 card (15 mi total): Mon rest, Tue 3.5mi easy, Wed 3mi+Strength A, Thu rest, Fri 3mi+strides+Strength B, Sat 7mi long, Sun Strength C/rest
- Week 2 card (17 mi total): with all 7 days
- Week 3 card (19 mi total): first 5th running day, gentle incline exposure
- Week 4 card (14 mi — STEP-BACK): with badge
- Week 5 card (22 mi total): return to progression, first double-digit long run 10mi
- Phase assessment paragraph about expected adaptations

Each week card uses the `.week-card` component from Task 5. Each day row includes session name, distance, HR targets, pace ranges, and treadmill alternatives in `.treadmill` spans. Quality sessions (strides) use `.day-row-quality`, long runs use `.day-row-long`, rest days use `.day-row-rest`.

- [ ] **Step 2: Verify in browser**

Scroll to Phase 1 — verify all 5 week cards render with correct color coding, mileage badges, step-back badge on week 4, treadmill alternatives visible.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: Phase 1 Base Building - weeks 1-5 with full training details"
```

---

### Task 7: Phase 2 — Build (Weeks 6-10)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Phase 2 section HTML**

Replace the empty `<section id="phase-2">` with the complete Phase 2 section containing:
- Phase header: "PHASE 2 — BUILD" with "Weeks 6-10 · 24→33 mi/wk"
- Phase intro (quality workouts begin, 80/20 rule, hill repeats, eccentric work)
- Week 6 card (24 mi): first hill repeats (5×30s), 11mi long run
- Week 7 card (27 mi): first tempo run (20min), 13mi long run (first over 2hrs)
- Week 8 card (20 mi — STEP-BACK): with badge, reduced volume
- Week 9 card (30 mi): two quality sessions, first downhill conditioning, MP segments
- Week 10 card (33 mi): tempo+hills combo, 16mi long run (longest ever milestone)
- Phase assessment (expected easy pace, tempo pace benchmarks)

Quality sessions (hill repeats, tempo, MP segments) use `.day-row-quality`. Each includes detailed HR targets, paces, treadmill settings.

- [ ] **Step 2: Verify in browser**

Scroll to Phase 2 — verify all 5 week cards, quality sessions are orange-accented, step-back badge on week 8.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: Phase 2 Build - weeks 6-10 with tempo, hills, marathon pace"
```

---

### Task 8: Phase 3 — Peak (Weeks 11-14)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Phase 3 section HTML**

Replace the empty `<section id="phase-3">` with:
- Phase header: "PHASE 3 — PEAK" with "Weeks 11-14 · 36→40 mi/wk"
- Phase intro (hardest phase, mileage peaks at 40, race-specific simulation, eccentric peak)
- Week 11 card (36 mi): SF course simulation hills, first MP long run (18mi with MP block miles 13-16)
- Week 12 card (27 mi — STEP-BACK): with badge, optional 10K race
- Week 13 card (38 mi): late-race hill simulation, 19mi course simulation long run (most important workout)
- Week 14 card (40 mi — PEAK WEEK): tempo+MP combo, 20mi peak long run
- Phase assessment

- [ ] **Step 2: Verify in browser**

Verify all 4 week cards, step-back badge on week 12, peak week emphasis on week 14.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: Phase 3 Peak - weeks 11-14 with race simulations and 40mi peak"
```

---

### Task 9: Phase 4 — Taper + Race Week (Weeks 15-17)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Phase 4 section HTML**

Replace the empty `<section id="phase-4">` with:
- Phase header: "PHASE 4 — TAPER" with "Weeks 15-17 · 30→Race"
- Phase intro (volume reduction 25%/week, maintain intensity, taper crazies normal)
- Week 15 card (30 mi): race-pace sharpener, 14mi last challenging long run
- Week 16 card (22 mi): final eccentric refresher, last hard workout (12min tempo), 10mi long run
- Week 17 card (Race Week — 14mi + 26.2): Mon-Sat shakeouts, Thu-Sat carb loading protocol, **Sunday RACE DAY** with full race morning timeline (3:00 AM wake, pre-race meal, gel before start)
- Race week card should have special styling — perhaps a subtle glow border or distinct background to mark it as the culmination

- [ ] **Step 2: Verify in browser**

Verify 3 week cards, race week stands out visually, carb loading days noted, race day morning timeline present.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: Phase 4 Taper - weeks 15-17 with race week and race morning"
```

---

### **CHECKPOINT: Phase 2 Complete**

Stop here. User scrolls through the entire page and reviews:
- All 17 weeks of training across 4 phases
- Color-coded session types (easy/quality/long/rest/strength)
- Step-back week badges
- Mileage badges on every week card
- Treadmill alternatives
- Phase intros and assessments
- Race week special styling

User confirms before proceeding to Phase 3.

---

## Phase 3: Supplementary Sections

### Task 10: SF Course Elevation Profile

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add course map HTML**

Replace the empty `<section id="course-map">` with a CSS-rendered elevation profile:
- Section header: "THE COURSE" with "26.2 miles · 1,303 ft elevation gain"
- A CSS elevation profile using a container div with child divs of varying heights and `clip-path` to create the mountain silhouette. Approximate the SF course: flat start (Embarcadero), sharp rise at mile 6-7 (GG Bridge, ~200ft), descent to Fort Baker, climb back at mile 12, rolling through Presidio, sustained climb miles 16-18 (GG Park), steep descent mile 20 (Haight), flat, then short hills at miles 23-24, flat finish.
- Mile markers along the bottom (every 2 miles)
- Key segment labels positioned above the profile at their respective mile locations: "Embarcadero", "GG Bridge", "Fort Baker", "Presidio", "Golden Gate Park", "Haight", "Mariposa Hills", "Finish"
- Elevation annotations at peaks (200ft at GG Bridge, 309ft at mile 15 peak) and valleys

Use a series of divs inside a flex container, each representing ~0.5 miles, with height proportional to elevation. Background gradient from `var(--surface)` to `var(--card)` with the profile shape created via `clip-path: polygon(...)` on a single container div.

- [ ] **Step 2: Add course map CSS**

Style the elevation profile, mile markers, segment labels, and elevation annotations. Use `var(--primary)` for the profile fill, with a gradient that fades toward the base.

- [ ] **Step 3: Verify in browser**

Verify elevation profile is visually readable, key segments are labeled, mile markers align.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: CSS elevation profile of SF Marathon course"
```

---

### Task 11: Race Day Execution Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add race day HTML**

Replace the empty `<section id="race-day">` with:
- Section header: "RACE DAY EXECUTION"
- Cardinal rule callout box: "Run by heart rate and effort, never by GPS pace" — styled as a prominent callout with `var(--danger)` left border and a warning-style background
- Race morning timeline: 3:00 AM wake → 2:00-2:30 AM pre-race meal → gel at -15min → 4:45 AM arrive corral → 5:15 AM start. Styled as a vertical timeline with time markers on the left.
- 7 segment strategy cards (miles 1-3, 4-8, 8-13, 13-18, 18-22, 23-24, 24-26.2), each containing: mile range, segment name, target HR range with zone color, target pace, key tactical notes. Use a consistent card layout with zone-colored left border.
- Fueling timeline table (9 rows: pre-start through mile 24.5, with timing, mile, action columns)
- Expected split times table for 4:00 finish (7 segments with miles, expected time, cumulative, notes)

- [ ] **Step 2: Add race day CSS**

Style the callout, timeline, segment cards, and tables.

- [ ] **Step 3: Verify in browser**

Verify all 7 segments render with correct zone colors, fueling table is readable, split times align.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: race day execution with segments, fueling, splits"
```

---

### Task 12: Hill Programming Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add hill programming HTML**

Replace the empty `<section id="hill-programming">` with:
- Section header: "HILL PROGRAMMING" with "From zero to SF-ready in 17 weeks"
- 4-stage progression displayed as a horizontal timeline or vertical stepper:
  - Stage 1 — Familiarization (Wk 3-5): gentle 2-4% inclines, walk downhills
  - Stage 2 — Structured Introduction (Wk 6-8): short repeats, first downhill exposure, eccentric exercises
  - Stage 3 — Race-Specific Building (Wk 9-13): long repeats at tempo, structured downhill repeats, RBE conditioning
  - Stage 4 — Maintenance (Wk 14-16): hill volume in long runs, final RBE refresher
- Treadmill course simulation table (6 rows: GG Bridge approach, Fort Baker return, GG Park climb, Late-race hills, Mile 15 descent, Haight descent — each with TM speed, incline, duration)
- Repeated Bout Effect callout: explanation of how eccentric exercise protects against future muscle damage

- [ ] **Step 2: Verify and commit**

```bash
git add index.html
git commit -m "feat: hill programming with 4-stage progression and TM simulations"
```

---

### Task 13: Strength Program Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add strength HTML**

Replace the empty `<section id="strength">` with:
- Section header: "STRENGTH PROGRAM" with "From 6x PPL to runner-optimized"
- Weekly frequency table (Weeks 1-5 through 16-17, with frequency, format, load, duration columns)
- Exercise cards (6 exercises): Bulgarian split squat, Single-leg RDL, Single-leg calf raise, Eccentric step-down, Copenhagen plank, Dead bug — each with sets/reps/tempo and purpose
- "Exercises to drop" callout: chest flies, lateral raises, bicep curls, tricep extensions, leg extensions, leg curls — with explanation of why (mass costs 2 sec/mi)
- Scheduling rule callout: lift on easy-run days, 6+ hours apart, never before long run/tempo/hills

- [ ] **Step 2: Verify and commit**

```bash
git add index.html
git commit -m "feat: strength program with exercises and weekly frequency"
```

---

### Task 14: Nutrition & Fueling Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add nutrition HTML**

Replace the empty `<section id="nutrition">` with:
- Section header: "NUTRITION & FUELING"
- Race-day gel visual strip: a horizontal bar representing 26.2 miles with gel markers at miles 0 (pre-start), 3, 7, 10.5, 14, 17, 20.5, 22 (caffeinated), 24.5 — styled as dots on a timeline with mile labels. Caffeine gels highlighted differently.
- Target: 60-80g carbs/hour, 8-9 gels total (200-270g carbohydrate)
- Carb loading protocol: 3-day table (Thu/Fri/Sat) with target carbs (788-946g/day at 10-12 g/kg), food suggestions, timing
- Pre-race meal spec: 2 bagels + jam + banana + 16oz sports drink = ~150-200g carbs, 3 hours before start
- Training fueling progression: when gels are introduced (week 5 first gel practice, week 7 two gels, week 9+ full race protocol)

- [ ] **Step 2: Verify and commit**

```bash
git add index.html
git commit -m "feat: nutrition section with gel timeline and carb loading"
```

---

### Task 15: Risk Management Section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add risk management HTML**

Replace the empty `<section id="risk-management">` with:
- Section header: "RISK MANAGEMENT"
- Daily monitoring protocol: RHR baseline ~49 bpm, HRV baseline 91-106 ms, track 7-day rolling averages
- Red flags grid (5 cards, each with red left border):
  - RHR elevated 5+ bpm for 3 days → cut mileage 30%, drop quality
  - HRV trending down 5+ days → extra rest day, reduce long run 20%
  - Sharp/localized pain → stop immediately, 2-3 days off, physio if persists
  - Easy-run HR 10+ bpm high → 2 rest days
  - Persistent fatigue/mood/sleep disruption 3+ days → step-back week
- Mileage adjustment rules (never increase >10% above recent peak, miss 5 days → resume at 70%, miss 10 days → restart current phase)
- Shoe strategy: replace every 300-350 miles at 78.8 kg, rotate 2 pairs, break in race shoes by week 12
- Critical injury-risk weeks callout: weeks 5-7, 9-11, 14 — with explanation of why each window is risky

- [ ] **Step 2: Verify and commit**

```bash
git add index.html
git commit -m "feat: risk management with red flags, monitoring, shoe strategy"
```

---

### **CHECKPOINT: Phase 3 Complete**

Stop here. User reviews all supplementary sections:
- CSS elevation profile of the course
- Race day execution (7 segments, fueling, splits)
- Hill programming (4 stages, TM simulations)
- Strength program (exercises, frequency, PPL transition)
- Nutrition (gel timeline, carb loading)
- Risk management (red flags, monitoring)

User confirms before proceeding to Phase 4.

---

## Phase 4: Polish

### Task 16: CSS Scroll Animations

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add scroll-driven animation CSS**

Add CSS for fade-in-on-scroll using `animation-timeline: view()`:

```css
/* Progressive enhancement: elements visible by default */
.animate-on-scroll {
  opacity: 1;
  transform: translateY(0);
}

/* Scroll-driven animations for supporting browsers */
@supports (animation-timeline: view()) {
  .animate-on-scroll {
    opacity: 0;
    transform: translateY(30px);
    animation: fade-in-up linear both;
    animation-timeline: view();
    animation-range: entry 0% entry 30%;
  }
}

@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

- [ ] **Step 2: Apply animation classes to HTML elements**

Add `class="animate-on-scroll"` to:
- All `.week-card` elements
- All phase headers
- All section headers in supplementary sections
- Phase summary cards in overview
- Race day segment cards
- Elevation profile container
- Strength exercise cards
- Red flag cards

- [ ] **Step 3: Add hover effects**

```css
.week-card {
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.week-card:hover {
  transform: translateY(-2px);
  border-color: rgba(255, 106, 0, 0.3);
}

.phase-card {
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.phase-card:hover {
  transform: translateY(-2px);
  border-color: var(--primary);
}
```

- [ ] **Step 4: Verify in Chrome**

Open in Chrome (115+) — scroll through entire page, verify elements fade in as they enter viewport. Open in Safari — verify all content is visible (no hidden elements).

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: CSS scroll animations with progressive enhancement"
```

---

### Task 17: Responsive Design

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add responsive CSS**

Add media queries for tablet and mobile:

```css
/* Tablet */
@media (max-width: 1024px) {
  .phase-cards { grid-template-columns: 1fr 1fr; }
  .hero-title { letter-spacing: -2px; }
  .section { padding: 80px 0; }
}

/* Mobile */
@media (max-width: 768px) {
  .phase-cards { grid-template-columns: 1fr; }
  .hero-stats { flex-direction: column; gap: 16px; }
  .hero-stat-separator { width: 40px; height: 1px; }
  .hero-title { letter-spacing: -1px; }
  .section { padding: 64px 0; }
  .container { padding: 0 16px; }
  .day-table td { padding: 10px 16px; font-size: 13px; }
  .day-table .day-details { font-size: 12px; }
  .nav-progress { display: none; }
  .week-card-header { flex-wrap: wrap; gap: 8px; }
  .elevation-profile { overflow-x: auto; }
  .hero-countdown-number { font-size: 48px; }
}
```

- [ ] **Step 2: Verify at 3 breakpoints**

Open in browser, resize to: 1200px (desktop), 900px (tablet), 375px (mobile). Verify layout adapts, no horizontal overflow, all content readable.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: responsive design for tablet and mobile"
```

---

### Task 18: Final Typography and Spacing Polish

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Review and refine**

Full visual pass through the page:
- Verify consistent spacing between all sections (120px desktop, 80px tablet, 64px mobile)
- Verify all phase headings use the same size/weight/spacing
- Verify all data values (pace, HR, zones) use JetBrains Mono
- Verify zone colors are applied consistently (Z2=green, Z3=yellow, Z4=orange, Z5=red)
- Verify all tables have consistent cell padding and border styling
- Check that no text is pure white on dark — body text should be `var(--text-secondary)` (#CCC), only headings use `var(--text-primary)` (#FFF)
- Add a footer at the bottom: "Built for the San Francisco Marathon · July 27, 2026" in muted text

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "polish: typography, spacing, and footer refinements"
```

---

### **CHECKPOINT: Phase 4 Complete — Deploy Ready**

Stop here. Final review:
- Scroll animations work in Chrome/Edge
- Content visible in all browsers (progressive enhancement)
- Responsive at all breakpoints
- Hover effects on cards
- Consistent typography and color throughout
- Footer present

User confirms the site is complete.

---

## Summary

| Phase | Tasks | What it delivers |
|-------|-------|-----------------|
| Phase 1 | Tasks 1-4 | Theme, nav, hero, overview |
| Phase 2 | Tasks 5-9 | All 17 training weeks |
| Phase 3 | Tasks 10-15 | Course map, race day, hills, strength, nutrition, risk |
| Phase 4 | Tasks 16-18 | Animations, responsive, polish |

Total: **18 tasks across 4 phases with 4 user checkpoints**.
