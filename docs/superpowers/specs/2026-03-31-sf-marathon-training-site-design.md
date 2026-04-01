# SF Marathon 17-Week Training Plan — Website Design Spec

**Date**: 2026-03-31
**Status**: Draft

---

## Summary

A single-file (`index.html`) cinematic vertical-scroll website presenting a 17-week San Francisco Marathon training plan. Dark & Athletic visual theme. Pure HTML/CSS — no JavaScript frameworks. CSS-only scroll animations. Designed for maximum visual impact and easy hosting.

---

## Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Visual direction | Dark & Athletic | Black/charcoal backgrounds, neon orange/red accents, bold typography, data-dashboard aesthetic |
| Page structure | Vertical Scroll Epic | One continuous cinematic scroll with sticky nav tracking position |
| Interactivity | Static Showcase (HTML/CSS only) | Content is the star. CSS-only animations. Zero dependencies, zero build step |
| Tech approach | Single HTML file | Maximum portability. Open in any browser, deploy anywhere. One file grows richer each phase |
| Content scope | All 7 supplementary sections + 17 training weeks | Hero, Overview, 4 Phases (17 weeks), Course Map, Race Day, Hills, Strength, Nutrition, Risk |

---

## Visual System

### Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--base` | `#0A0A0A` | Page background |
| `--surface` | `#111111` | Section backgrounds |
| `--card` | `#1A1A1A` | Card/panel backgrounds |
| `--border` | `#2A2A2A` | Subtle borders |
| `--text-primary` | `#FFFFFF` | Headings, key data |
| `--text-secondary` | `#CCCCCC` | Body text |
| `--text-muted` | `#888888` | Labels, captions |
| `--text-dim` | `#555555` | Inactive states |
| `--primary` | `#FF6A00` | Neon orange — phase accents, CTAs, active states |
| `--danger` | `#FF3B30` | Red — HR zones, warnings, Z5 |
| `--success` | `#34C759` | Green — race-day sections, completed states |
| `--warning` | `#FFD60A` | Yellow — caution, Z4 markers |
| `--z2` | `#34C759` | Zone 2 — green |
| `--z3` | `#FFD60A` | Zone 3 — yellow |
| `--z4` | `#FF6A00` | Zone 4 — orange |
| `--z5` | `#FF3B30` | Zone 5 — red |

### Typography

| Role | Font | Weight | Size | Style |
|------|------|--------|------|-------|
| Phase headings | Inter | 900 (Black) | 48-64px | Uppercase, letter-spacing -2px |
| Section titles | Inter | 700 (Bold) | 28-36px | Normal case |
| Week headings | Inter | 600 (Semi-bold) | 20-24px | Normal case |
| Body text | Inter | 400 (Regular) | 15-16px | Line-height 1.7 |
| Data/metrics | JetBrains Mono | 500 (Medium) | 13-16px | Tabular numerals, orange accent |
| Labels | Inter | 600 | 11px | Uppercase, letter-spacing 3px |

Fonts loaded via Google Fonts (`<link>` tags). Fallback: `system-ui, -apple-system, sans-serif` / `monospace`.

### Spacing & Layout

- Max content width: `900px` centered
- Section vertical padding: `120px` top/bottom (generous breathing room)
- Card padding: `24-32px`
- Card border-radius: `12px`
- Consistent `16px` grid unit for spacing

---

## Page Sections (Scroll Order)

### 1. Hero (full viewport)

- Full-height viewport (`100vh`)
- Race name "SAN FRANCISCO MARATHON" in massive bold type
- Subtitle: "17-Week Training Plan"
- Countdown: days until race (July 27, 2026) — static number, calculated at build time
- Three stat pills: `VO2max: 51.6` | `Current: 13 mi/wk` | `Target: 4:00`
- Subtle gradient background with radial glow accent
- Scroll indicator arrow at bottom

### 2. Overview / Periodization

- 4 phase summary cards in a row (responsive: stack on mobile)
- Each card: phase name, week range, mileage range, focus keywords
- Periodization architecture table (Phase / Weeks / Focus / Mileage / Runs / Strength)
- Goal calibration paragraph with the 4:00 primary / 3:45 stretch targets

### 3-6. Training Phases (×4)

Each phase section follows the same template:

- **Phase header**: Large phase name + week range + mileage range
- **Phase intro**: 2-3 paragraph explanation of the phase's purpose and focus
- **Week cards**: One card per week containing:
  - Week number + total mileage badge
  - "STEP-BACK" badge for recovery weeks (weeks 4, 8, 12)
  - 7-day table: Day | Session name | Distance | Key details
  - Each day row uses color-coded session type:
    - Easy Run → muted/default
    - Quality workout (tempo, hills, MP) → orange accent
    - Long Run → orange border, slightly larger
    - Rest → dim
    - Strength → subtle icon/label
  - Treadmill alternatives shown inline with outdoor instructions
- **Phase assessment**: End-of-phase fitness benchmarks

### 7. SF Course Map / Elevation Profile

- CSS-rendered elevation profile (using `clip-path` or layered `div` bars to approximate the 26.2-mile profile)
- Key segments labeled: GG Bridge, Fort Baker, Golden Gate Park, Haight-Ashbury, Mariposa Hills
- Elevation numbers at peaks and valleys
- Mile markers along the bottom axis
- Total elevation gain callout: 1,303 ft

### 8. Race Day Execution

- Mile-by-mile segment strategy (7 segments with target HR, pace, and tactical notes)
- Fueling timeline table (timing, mile, action)
- Expected split times table for 4:00 finish
- Race morning timeline (3:00 AM wake → 5:15 AM start)
- Cardinal rule callout: "Run by heart rate, never by GPS pace"

### 9. Hill Programming

- 4-stage progression summary (Familiarization → Introduction → Race-specific → Maintenance)
- Treadmill course simulation table (SF segment → TM settings)
- Repeated Bout Effect explanation callout

### 10. Strength Program

- Weekly frequency table across all 17 weeks
- Exercise list with sets/reps/tempo for each movement
- "Exercises to drop" section (PPL transition)
- Scheduling rule: lift on easy-run days, 6+ hours apart

### 11. Nutrition & Fueling

- Race-day gel timeline (visual strip with mile markers)
- Carb loading protocol (Thu/Fri/Sat before race)
- Pre-race meal spec
- Training fueling practice progression (when gels are introduced in long runs)

### 12. Risk Management

- Daily monitoring protocol (RHR/HRV baselines and red flags)
- Red flags list with immediate actions
- Mileage adjustment rules
- Shoe strategy (rotation, replacement cadence)
- Critical injury-risk weeks highlighted

---

## Sticky Navigation

- Thin bar (`48px`) fixed at top of viewport
- Left: site title "SF MARATHON PLAN"
- Center: scroll progress bar (thin horizontal line that fills left-to-right as user scrolls, using CSS `animation-timeline: scroll()`). Section name tracking would require JS, so each section instead has a large, unmistakable header visible as you scroll.
- Right: race day countdown ("118 DAYS")
- Background: `#0A0A0A` with slight transparency (`rgba(10,10,10,0.9)`) and `backdrop-filter: blur(8px)`

**Note**: CSS `animation-timeline: scroll()` enables a progress bar without JS. Section name tracking requires JS, so instead we show section names as visible labels within the content itself — each section has a large, unmistakable header.

---

## CSS Animations (CSS-only)

- **Fade-in on scroll**: Using `@keyframes` with `animation-timeline: view()` — elements fade/slide up as they enter viewport. Applied to week cards, stat numbers, phase headers.
- **Progress bar**: Sticky nav progress bar fills via `animation-timeline: scroll()`.
- **Hover effects**: Cards lift slightly (`transform: translateY(-2px)`) with border glow on hover.
- **Gradient shifts**: Subtle background gradient transitions on phase sections.
- **Pulse**: Race countdown number has a subtle pulse animation.

Browser support: `animation-timeline` works in Chrome 115+ and Edge. For Safari/Firefox fallback, elements remain visible without animation (progressive enhancement — content is never hidden by default).

---

## Responsive Behavior

- **Desktop (>1024px)**: Full layout, 900px max-width content, side-by-side cards
- **Tablet (768-1024px)**: Slightly narrower, 2-column card grids become 1-column where needed
- **Mobile (<768px)**: Single column, phase cards stack, week tables become card layouts, font sizes scale down ~15%, section padding reduces to 80px

---

## Build Phases (Implementation Checkpoints)

### Phase 1: Foundation
- HTML document structure with all 12 sections as empty `<section>` elements
- Full CSS theme system (custom properties, typography, colors)
- Sticky navigation bar with scroll progress
- Hero section fully designed and populated
- Overview/periodization section
- **Checkpoint**: User reviews foundation + hero + overview

### Phase 2: Training Weeks
- All 17 weeks across 4 training phase sections
- Week card component with day tables
- Color-coded session types
- Step-back week badges
- Phase intro text and end-of-phase assessments
- **Checkpoint**: User reviews all training content

### Phase 3: Supplementary Sections
- SF Course elevation profile (CSS-rendered)
- Race Day Execution (segments, fueling, splits)
- Hill Programming section
- Strength Program section
- Nutrition & Fueling section
- Risk Management section
- **Checkpoint**: User reviews all supplementary content

### Phase 4: Polish
- CSS scroll animations (`animation-timeline: view()` and `scroll()`)
- Hover effects and micro-interactions
- Responsive breakpoints (tablet + mobile)
- Final typography and spacing refinements
- Progressive enhancement fallbacks
- **Checkpoint**: Final review, deploy-ready

---

## File Structure

```
marathonplan/
├── index.html          # The entire site — single file
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-03-31-sf-marathon-training-site-design.md  # This spec
```

---

## Out of Scope

- JavaScript frameworks (React, Vue, etc.)
- Build tools or bundlers
- Backend or API
- User accounts or login
- Dynamic data or CMS
- Service worker or PWA features
- Dark/light mode toggle (always dark)
