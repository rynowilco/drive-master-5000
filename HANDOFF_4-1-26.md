# Drive Master 5000 — Complete Development Brief & v3 Handoff

---

## ✉️ PROMPT FOR YOUR NEXT AI ASSISTANT

Copy and paste everything below this line as your opening message:

---

Hi! I need your help continuing development on a project called **Drive Master 5000** — a mobile web quiz app built to help my son Tyler (turning 15) study for his Oregon DMV learner's permit test.

I'm not a developer, so I need clear step-by-step guidance and complete files — no partial code snippets for me to hunt down and edit.

**Please read this entire brief before asking any questions or writing any code.** It covers everything that's been built, every technical decision that's been made, the current state of the app, and ideas for what comes next.

---

## PROJECT OVERVIEW

**Drive Master 5000** is a single-file mobile web app (`index.html`) hosted on GitHub Pages. It requires no installation, no accounts, no authentication of any kind. Tyler opens a link in his phone browser and plays. Progress saves automatically via the browser's built-in `localStorage`.

Each user's progress is stored entirely on their own device — the app runs locally, nothing is sent to any server, and multiple people can use the same URL simultaneously without interfering with each other.

**Design aesthetic:** Dark gamer theme with San Francisco 49ers colors — scarlet (`#C8102E`) and gold (`#B3995D`) on a near-black background (`#080808`). Typography: Bebas Neue (headers/numbers) + Barlow (body), loaded from Google Fonts.

**Source material:** The Oregon Driver Manual 2026–2027 (Class C non-commercial driving privilege). All questions and study content must be derived from this manual only.

**Hosting:** GitHub Pages (free). Single `index.html` at repository root.
Tyler accesses via `https://[username].github.io/drive-master-5000/`

---

## WHAT'S BEEN BUILT — COMPLETE FEATURE LIST

### v1 Features (shipped first)

**5 Active Game Modes:**

| Mode | Description |
|---|---|
| **Classic Quiz** | 35 shuffled questions, need 28/35 to pass — mirrors the real DMV test |
| **Sign Blitz** | Signs & signals questions only (18 eligible), 10-second countdown per question, speed bonus XP if answered with 6+ seconds remaining, auto-wrong on timeout |
| **Streak Mode** | Endless shuffled questions, one wrong answer ends the run, streak counter glows red at 5+, loops through all 100 questions indefinitely |
| **Weak Spots Drill** | Auto-pulls every question Tyler has ever answered wrong, clears each one as he gets it right, shows empty state if no weak spots yet |
| **Boss Battle** | 35 questions with an 8-minute countdown clock, clock turns red and pulses in final 60 seconds, time-out triggers results screen |

**Gamification System:**
- XP earned after every session (rates vary by mode — see XP Rates section below)
- 10 levels with named ranks: Learner's Permit → Parking Lot Pro → Neighborhood Navigator → Street Certified → Road Runner → Highway Hero → Traffic Tamer → Permit Master → Road Scholar → DRIVE MASTER 5000 👑
- Level-up overlay fires when a level is gained — full-screen celebration with 49ers scarlet/gold confetti (55 animated dots, pure CSS)
- Animated XP bar with shimmer sweep effect on the home screen
- Toast notifications (non-blocking, 2.8s auto-dismiss) used for all user messages — no `alert()` anywhere

---

### v2 Features (current version — fully shipped)

**The On-Ramp: Your Driving Test Study Guide** — a complete study system added alongside the existing quiz modes.

**How it fits into the app:**
- The On-Ramp card now sits at the TOP of the home screen mode list (moved from bottom placeholder position)
- Card uses sky-blue (`t-teal`) styling to visually distinguish it from the quiz modes
- Tapping it navigates to the `#study` chapter-select screen

**The study flow has three screens:**

**1. Chapter Select (`#study`)**
- Hero strip with overall progress bar (0–100% as chapters are read)
- 9 chapter cards built dynamically from the `CHAPTERS` data array
- Unread chapters show `+25 XP` reward hint and a `›` arrow
- Read chapters flip to green checkmark style — teal accent bar turns green, label updates to "✅ Read"
- Chapter count in top bar (e.g., "3 / 9")

**2. Chapter Viewer (`#chapter`)**
- Chapter number + name in top bar
- Scrollable content built from structured `CHAPTER_CONTENT` blocks (see data section below)
- Three content block types: `heading` (teal, Bebas Neue), `text` (body copy), `callout` (gold highlight box)
- A fourth type `signs` renders inline SVG road signs using the existing `SIGNS` renderer
- **Three buttons at the bottom:**
  - ✅ **Mark as Read · +25 XP** — teal button, awards XP once on first read, permanently flips to "Chapter Complete" after tapping
  - 🪞 **Check the Rearview Mirror** — gold-tinted button, launches 10-question chapter mini-quiz
  - ← **Back to Chapters** — returns to chapter select screen

**3. Rearview Mirror Quiz**
- Uses the full existing `#game` screen and engine — no separate UI needed
- Chapter name appears in the game top bar instead of a mode name
- Questions drawn from `CHAPTER_CATS` mapping (see data section), shuffled fresh each attempt
- Up to 10 questions per quiz (some chapters have fewer — all are used when pool < 10)
- Results screen shows chapter-specific headlines: Perfect / Nailed It / Almost There / Keep Studying
- "Retake Quiz" button re-runs the same chapter with a fresh shuffle
- XP: 10 per correct, 2 per wrong, +20 bonus for 80%+ score

---

## THE 9 ON-RAMP CHAPTERS

All content sourced strictly from the Oregon Driver Manual 2026–2027.

| # | Chapter | Key Topics | Signs Shown | Quiz Pool |
|---|---|---|---|---|
| 0 | Road Signs 101 | Shapes, colors, regulatory/warning/info/service types, red-slash rule | stop, yield, school, railroad, donotenter, warning, speedlimit | 10 of 18 Signs questions |
| 1 | Traffic Signals | Steady/flashing red/yellow/green, yellow arrow, dark signal | — | All 8 Signals questions |
| 2 | Speed Laws | Default limits by zone, Basic Rule, work zone doubles | — | All 8 Speed questions |
| 3 | Lane Rules & Markings | Yellow/white lines, HOV, bike lanes, freeway merging | — | All 7 Lane Travel questions |
| 4 | Space Cushion | 2-4 second rule, stopping distance at 55 mph, backing up | — | All 5 Space Cushion questions |
| 5 | Turns & Intersections | Signal 100ft, right/left turn technique, red-light turns, right-of-way, roundabouts | — | 10 of 11 Turns + Roundabouts questions |
| 6 | Sharing the Road | Pedestrians (all crosswalks), cyclists (3ft/35mph rule), school buses, emergency vehicles, large trucks, transit buses | — | 10 of 18 across 6 categories |
| 7 | Parking Rules | 12-inch curb rule, hill parking wheel directions, no-park distances, disabled permit fines | — | All 6 Parking questions |
| 8 | Safe & Responsible Driving | Seat belts, child seats, cell phone laws, BAC limits, Implied Consent, skidding, collision avoidance | — | All 10 Safe Driving questions |

---

## XP RATES BY MODE

| Mode | Per Correct | Per Wrong | Bonus |
|---|---|---|---|
| Classic Quiz | 10 XP | 2 XP | +50 XP for passing (28+/35) |
| Boss Battle | 10 XP | 2 XP | +50 XP for passing |
| Sign Blitz | 8 XP | 1 XP | +5 XP speed bonus (answer with 6s+ remaining) |
| Streak Mode | 15 XP × multiplier | — | Multiplier = 1 + (streak × 0.05) |
| Weak Spots Drill | 12 XP | 2 XP | — |
| Rearview Mirror | 10 XP | 2 XP | +20 XP for 80%+ score |
| Read a Chapter | — | — | +25 XP flat (first read only, no repeat award) |

---

## LEVEL SYSTEM

| Level | Rank | XP Required |
|---|---|---|
| 1 | Learner's Permit 🚗 | 0 |
| 2 | Parking Lot Pro 🅿️ | 100 |
| 3 | Neighborhood Navigator 🏘️ | 250 |
| 4 | Street Certified 📋 | 500 |
| 5 | Road Runner 🏃 | 900 |
| 6 | Highway Hero 🛣️ | 1,500 |
| 7 | Traffic Tamer 🚦 | 2,400 |
| 8 | Permit Master 🎯 | 3,600 |
| 9 | Road Scholar 📚 | 5,200 |
| 10 | DRIVE MASTER 5000 👑 | 7,500 |

---

## PERSISTENCE (localStorage)

**Key:** `dm5000_v2`

The key was bumped from `dm5000_v1` to `dm5000_v2` when `chaptersRead` was added to the schema. If the save schema changes again in future, bump to `dm5000_v3`.

**Saved fields:**

| Field | Type | Description |
|---|---|---|
| `xp` | number | Total XP earned all-time |
| `bestStreak` | number | Highest streak ever achieved |
| `totalRight` | number | Total correct answers all-time |
| `totalAnswered` | number | Total questions answered all-time |
| `weakIds` | array | IDs of questions Tyler has answered wrong |
| `sessions` | number | Total quiz sessions played |
| `chaptersRead` | array | Chapter IDs (0–8) read at least once |

All fields are validated on load — type-checked and range-checked. Corrupt or missing saves fail gracefully and start fresh. Quota errors on write fail silently.

**Note on progress loss:** Tyler's save is tied to his browser's localStorage. If he clears browser data or switches browsers, progress resets. This is the primary limitation of the localStorage approach.

---

## TECHNICAL ARCHITECTURE

```
index.html  (single file, ~2,180 lines, no dependencies except Google Fonts)
│
├── <head>              Meta tags, PWA tags, emoji favicon (🏆), Google Fonts link
├── <style>             All CSS (~570 lines) using CSS custom properties
│
├── #home               Home screen HTML
├── #game               Game screen HTML — all HUDs in DOM, shown/hidden by JS
├── #results            Results screen HTML
├── #study              Chapter-select screen HTML (v2)
├── #chapter            Chapter-viewer screen HTML (v2)
├── #levelup-overlay    Level-up celebration overlay
├── .confetti-wrap      Confetti animation container
├── #toast              Toast notification element
│
├── <script> block 1    Data layer:
│                         QUESTIONS array (100 objects)
│                         SIGNS SVG map (8 sign types)
│                         CATEGORIES array (18 categories with name/color/icon)
│                         CHAPTERS array (9 On-Ramp chapter metadata objects)
│                         CHAPTER_CATS array (9 category-filter arrays for quizzes)
│                         CHAPTER_CONTENT array (9 arrays of content blocks)
│
└── <script> block 2    Engine (~700 lines):
                          Constants, state, localStorage,
                          XP/levels, all 6 mode launchers + timer logic,
                          question renderer, answer handler,
                          results builder, level-up + confetti,
                          On-Ramp navigator + chapter renderer,
                          markChapterRead + XP award,
                          startChapterQuiz (Rearview Mirror),
                          toast, screen nav, shuffle, reset, install tip
```

---

## KEY CSS CUSTOM PROPERTIES

All defined in `:root`. Never hardcode hex values in component CSS rules.

```css
/* Brand */
--red: #C8102E          --red-dk: #AA0000       --red-glow: rgba(200,16,46,.32)
--gold: #B3995D         --gold-lt: #D4B97A      --gold-bright: #F0D090
--gold-dk: #8A7240      --gold-glow: rgba(179,153,93,.28)

/* Teal (On-Ramp / study system — added v2) */
--teal: #0EA5E9         --teal-lt: #7DD3FC      --teal-glow: rgba(14,165,233,.25)

/* Backgrounds & surfaces */
--bg: #080808           --bg2: #0E0E10
--surf: #141418         --surf2: #1C1C22        --surf3: #242430

/* Borders */
--border: #2A2A36       --border-lt: #3A3A4A    --border-gold: #4A4030

/* Text */
--text: #F0F0F2         --dim: #888899          --faint: #444458

/* Feedback */
--correct: #22C55E      --correct-bg: rgba(34,197,94,.12)
--wrong: #EF4444        --wrong-bg: rgba(239,68,68,.10)

/* Radii */
--r: 12px               --rsm: 8px
```

---

## KEY JS FUNCTIONS

**Screen navigation:**
```
showScreen(id)           — deactivates all screens, activates target, scrolls to top
goHome()                 — clears timers, reloads progress, shows #home
openStudyGuide()         — calls renderStudySelect(), shows #study
openChapter(id)          — renders chapter content + sets up buttons, shows #chapter
closeChapter()           — calls openStudyGuide() (back to chapter list)
```

**Quiz engine:**
```
startMode(mode)          — launcher for all 6 modes (classic/signblitz/streak/
                           weakspots/boss/rearview). Accepts optional filter via
                           state._chapterId for rearview mode.
startChapterQuiz(id)     — sets state._chapterId, calls startMode('rearview')
renderQuestion()         — builds question UI from state.queue[state.idx]
handleAnswer(chosen, q)  — scores answer, updates state, shows feedback
nextQuestion()           — advances idx, restarts timers if needed
showResults()            — calculates XP, populates results screen, checks level-up
playAgain()              — restarts current mode (rearview re-uses same chapter id)
```

**On-Ramp / study system:**
```
renderStudySelect()      — builds chapter card list from CHAPTERS + chaptersRead state
openChapter(id)          — renders chapter content blocks from CHAPTER_CONTENT[id]
markChapterRead()        — awards 25 XP (first time only), saves, updates button state
startChapterQuiz(id)     — filters QUESTIONS by CHAPTER_CATS[id], launches rearview mode
```

**XP / levels:**
```
getLevel(xp)             — returns level number (1–10) for given XP value
getLevelProgress(xp)     — returns { lv, cur, next, pct } for XP bar rendering
updateHomeXP()           — refreshes all home screen stat displays
animateXPBar(from, to)   — animates XP bar fill on home screen return
checkLevelUp(old,new,xp) — fires level-up overlay + confetti if level increased
closeLevelUp()           — dismisses overlay, clears confetti, fires callback
```

**Persistence:**
```
saveProgress()           — writes persistent fields to localStorage (dm5000_v2)
loadProgress()           — reads + validates save from localStorage
resetProgress()          — clears localStorage, resets all state fields
```

**Utilities:**
```
shuffle(arr)             — Fisher-Yates shuffle, returns new array
showToast(msg)           — non-blocking toast, auto-dismisses after 2.8s
spawnConfetti()          — creates 55 animated confetti dots (CSS animation)
resetHUDs()              — hides all mode-specific HUD strips
showHUD(id)              — reveals a specific HUD strip
```

---

## QUESTION BANK

100 questions across 18 categories. Every question object:

```javascript
{
  id:   1,                        // unique integer
  cat:  "Signs",                  // category name — used by CHAPTER_CATS filters
  tags: ["sign", "regulatory"],   // "sign" tag = eligible for Sign Blitz
  sign: "stop",                   // optional — maps to SIGNS SVG renderer
  q:    "Question text",
  opts: ["Option A", "Option B", "Option C"],
  ans:  0,                        // 0-indexed correct answer
  exp:  "Explanation shown after answering",
  ref:  "Manual section, p.XX"
}
```

**Category counts:**
Signs (18), Safe Driving (10), Signals (8), Speed (8), Lane Travel (7), Turns (6), Parking (6), Roundabouts (5), Space Cushion (5), School Buses (4), Emergency Vehicles (3), Passing (3), Pedestrians (3), Railroad (3), Bicycles (3), Large Vehicles (3), Motorcycles (2), Work Zones (3).

**SVG signs available** (keys in `SIGNS` object):
`stop`, `yield`, `donotenter`, `warning`, `speedlimit`, `slippery`, `school`, `railroad`

---

## DATA ARRAYS (v2 additions)

**`CHAPTERS` array** — metadata for all 9 On-Ramp chapters:
```javascript
{ id: 0, icon: '🚦', name: 'Road Signs 101',
  desc: 'Shapes, colors & what every sign type means', xp: 25 }
// ... 8 more
```

**`CHAPTER_CATS` array** — maps chapter id → question category names:
```javascript
['Signs'],                                     // 0
['Signals'],                                   // 1
['Speed'],                                     // 2
['Lane Travel'],                               // 3
['Space Cushion'],                             // 4
['Turns', 'Roundabouts'],                      // 5
['Pedestrians','Bicycles','School Buses',
 'Emergency Vehicles','Large Vehicles',
 'Motorcycles'],                               // 6
['Parking'],                                   // 7
['Safe Driving'],                              // 8
```

**`CHAPTER_CONTENT` array** — 9 arrays of content block objects:
```javascript
// Block types:
{ t: 'heading', v: 'Section Title' }
{ t: 'text',    v: 'Body paragraph text.' }
{ t: 'callout', v: '🚦 Key fact in a gold box.' }
{ t: 'signs',   v: ['stop', 'yield'] }  // renders SVG sign row
```

---

## SCREENS IN THE DOM

| ID | Purpose | Navigated to by |
|---|---|---|
| `#home` | Home screen — mode select, XP bar, stats | `goHome()` |
| `#game` | Quiz screen — all 6 modes share this | `startMode()`, `startChapterQuiz()` |
| `#results` | Results screen | `showResults()` |
| `#study` | On-Ramp chapter select | `openStudyGuide()` |
| `#chapter` | Chapter viewer + Mark as Read + quiz launch | `openChapter(id)` |

All screens share `.screen` class. Only the active screen has `.active` class (set by `showScreen(id)`).

---

## DEVELOPMENT CONVENTIONS — MAINTAIN THESE

- **No partial code snippets.** Always provide complete files, or use targeted str_replace with exact unique strings. The owner is non-technical.
- **Build in named steps, verify each before proceeding.** Run Node.js syntax checks (`new Function(scriptContent)`) after every JavaScript edit.
- **Surgical edits only** — make the minimum change required. Never rewrite from scratch unless strictly necessary.
- **All colors via CSS custom properties** — never hardcode hex values in component CSS rules.
- **No `alert()`** — use `showToast(msg)` for all user-facing notifications.
- **No external dependencies** beyond Google Fonts. No jQuery, no React, no CDN scripts.
- **Version localStorage keys** when save schema changes (current: `dm5000_v2` — next would be `dm5000_v3`).
- **Comment all major JS sections** using the `/* ════ SECTION NAME ════ */` style already established.
- **Mobile-first.** Target 375px viewport. No hover-dependent functionality.
- When in doubt: **reliable, robust, and free** over clever.

---

## IMPORTANT CONTEXT

- **Tyler has ADHD.** Gamification, quick feedback loops, visual variety, and short bursts of content are key. Chapters should be scannable, not walls of text.
- **The app is personalized for Tyler** — results screens reference him by name. Maintain this tone.
- **The owner is non-technical.** All instructions must be plain-English, step-by-step, with no assumed knowledge.
- **The Oregon DMV knowledge test:** 35 multiple-choice questions, 3 options (A/B/C), 28 correct to pass.
- **Content accuracy is critical.** All questions and study content must be sourced from the Oregon Driver Manual 2026–2027 only. Do not invent or add rules not in that manual.
- **No Google authentication, no Firebase, no third-party accounts of any kind.** The app must remain fully self-contained. Previous attempts with authenticated tools caused problems.

---

## POTENTIAL v3 IDEAS

These were discussed or implied during v2 development but not yet built. None are started — all would begin from the current `index.html`.

- **Progress nudge on first launch** — if `state.sessions === 0`, show a prompt suggesting Tyler start with The On-Ramp before quizzing. The `sessions` counter is already saved.
- **Rearview quiz chapter return** — currently the "Home Base" button on rearview results goes to the home screen. A "Back to Chapter" secondary button that returns to the chapter viewer could be a nice touch.
- **Expanded question bank** — the existing 100 questions cover the manual well but more questions per category would improve Rearview quiz variety (especially for the 5-question categories like Space Cushion and Parking).
- **Daily challenge mode** — a fixed set of 10 questions that resets every 24 hours, same questions for all users that day. Encourages daily habit.
- **Accuracy milestone badges** — visual awards for hitting 75%, 85%, 95% lifetime accuracy, displayed on the home screen.
- **Chapter review prompt** — after Tyler fails a Rearview quiz, automatically offer to re-open the chapter before retrying.
- **Sound effects** — subtle audio feedback (correct chime, wrong buzz, level-up fanfare). Would need a user preference toggle.

---

## FILES

| File | Status | Purpose |
|---|---|---|
| `index.html` | ✅ Final v2 app | The only file needed — upload this to GitHub Pages |
| `HANDOFF.md` | ✅ This document | Full development brief for next AI assistant |

**For v3 development: start from `index.html` as your base. Read this entire brief first. Ask clarifying questions before writing any code.**

---

*Drive Master 5000 v2.0 — Built April 2026*
*Oregon Permit Prep · Built for Tyler*
*Good luck on the permit test, Tyler. The road is waiting. 🚗*
