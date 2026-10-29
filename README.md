# ENTC InnovateHub

A modern smart learning platform for Electronics and Telecommunication Engineering students.

## Features

- Student dashboard with mission progress graph
- Login and registration using Supabase Auth when configured; development-only demo access otherwise
- Interactive ENTC learning modules
- Virtual electronics lab with Ohm’s law, logic gates, LED circuit, and streetlight simulators
- Rule-based AI learning assistant examples (no live model or AI backend is configured)
- Arduino coding challenges with safe rule-based validation
- Timed quiz system with instant feedback
- CHAKRAVYUH mission track with XP, credits, stars, levels, achievements, and cosmetic unlocks
- CHAKRAVYUH Circuit Lab with a searchable component library, pin-level wiring, dragging, rotation, zoom/pan, undo/redo, save/load, SVG diagram and CSV bill-of-materials export
- Books Library with search, subject/author/semester/difficulty filters, details, official publisher websites, bookmarks, and reading status

## Getting started

1. Install dependencies:

```bash
npm install
```

2. Copy the environment template and add your Supabase credentials if available:

```bash
cp .env.example .env
```

3. Start the development server:

```bash
npm run dev
```

## Environment variables

The app checks for the following variables:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
```

The Supabase anon key is a public client key; database access must be protected by server-side policies. Never put a private AI-provider key in a `VITE_` variable. No secure AI backend is included. When Supabase credentials are missing, the app uses development-only demo authentication and clearly labelled educational examples.

## CHAKRAVYUH simulator and game progress

The Circuit Lab is integrated with the mission track. Component positions, properties, wires, and code are saved in this browser under the current account; this repository has authentication but no circuit database schema or project-sharing service. Export provides an SVG diagram and a CSV bill of materials.

The deterministic circuit simulator currently recognizes two circuit/code patterns:

- **Blink an LED:** Arduino D13 → resistor (220 Ω or greater) → LED anode; LED cathode → ground node → Arduino GND. The sketch must configure pin 13 as OUTPUT, write HIGH and LOW, and use a positive `delay()`.
- **Button-controlled LED:** Arduino D2 → push button → shared ground, plus the same D13/resistor/LED path. The sketch must use `INPUT_PULLUP`, read D2, and drive the LED on for LOW and off for HIGH. Use the virtual button control while the simulation is running.

No external Arduino runtime/compiler is integrated. The app does not compile or execute arbitrary Arduino C++. Starter sketches for sensors, servo, and other devices are examples only. Components labelled **visual model only** or **preview only** are not simulated and cannot be used to claim mission completion. The virtual multimeter only reports modeled nominal Arduino logic levels, resistor properties, or direct wire-graph continuity; other measurements are reported as unsupported.

The circuit suggestion assistant is a fixed rule-based template for Blink and button-controlled LED circuits, not an AI-generated design. Live model responses require a separately deployed secure backend.

## Books Library

The Books Library provides a starter catalogue, 22 ENTC subject filters, search, author/semester/difficulty/language/format filters, details, favorites, and reading statuses. No book files are hosted or redistributed. Links go to publisher websites; users should search for the exact title and use authorized access.

Bibliographic metadata such as edition, ISBN, publication year, publisher, and cover image is omitted unless verified. Starter records do not currently include verified edition identifiers, cover art, author biographies, tables of contents, popularity, or availability. They are catalogue guidance, not a claim that a particular edition is stocked or available as an ebook.

Bookmarks and reading statuses are stored in browser local storage, scoped by the signed-in email. There is no library database migration, cross-device synchronization, admin role/catalogue editor, ratings system, or server-verified reading reward in this project. Personal browser storage is not tamper-resistant.

In development/demo authentication mode, game progress is stored in this browser under the student's email, survives logout/login in that browser, and gives each mission rewards only once. This local progress is not tamper-resistant and must not be used for official grades, prizes, or competitive rankings. With Supabase configured, authentication can be server-backed, but this repository does not include a CHAKRAVYUH reward-verification RPC/database schema; consequently, the simulator will not issue XP or credits in that mode. A secure cross-device leaderboard and authoritative rewards require a separately deployed server-side validation service. Supabase configuration alone does not provide that feature.

The leaderboard is intentionally identified as unavailable until such a service is deployed. Daily dates and streaks use UTC. Optional hints and cosmetic unlocks are demo credit purchases.

## Build and validation

```bash
npm run build
npm run lint
```
