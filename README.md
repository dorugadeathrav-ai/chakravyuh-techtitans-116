# ENTC InnovateHub

A modern smart learning platform for Electronics and Telecommunication Engineering students.

## Features

- Landing page and responsive navigation
- Development-only authentication demo mode when Supabase is not configured
- Student dashboard with progress tracking and learning insights
- Interactive ENTC learning modules
- Virtual electronics lab with Ohm’s law, logic gates, LED circuit, and streetlight simulators
- AI learning assistant with demo educational responses when no backend keys are configured
- Arduino coding challenges with safe rule-based validation
- Timed quiz system with instant feedback
- CHAKRAVYUH mission track with XP, credits, stars, levels, achievements, and cosmetic unlocks
- Interactive Arduino circuit workspace with supported Blink and button-controlled LED missions

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

Optional future AI backend variables can be added as needed:

```env
VITE_OPENAI_API_KEY=your-key-if-configured
```

If credentials are missing, the app automatically falls back to a clearly labeled development-only demo mode and educational example responses rather than claiming live AI functionality.

## CHAKRAVYUH simulator and game progress

The circuit workspace currently simulates two deterministic circuit/code patterns:

- **Blink an LED:** Arduino D13 → resistor (220 Ω or greater) → LED anode; LED cathode → ground node → Arduino GND. The sketch must configure pin 13 as OUTPUT, write HIGH and LOW, and use a positive `delay()`.
- **Button-controlled LED:** Arduino D2 → push button → shared ground, plus the same D13/resistor/LED path. The sketch must use `INPUT_PULLUP`, read D2, and drive the LED on for LOW and off for HIGH. Use the virtual button control while the simulation is running.

Other entries in the mission track are previews and cannot run or award completion rewards. The simulator does not compile or execute arbitrary Arduino C++.

In development/demo authentication mode, game progress is stored in this browser under the student's email, survives logout/login in that browser, and gives each mission rewards only once. This local progress is not tamper-resistant and must not be used for official grades, prizes, or competitive rankings. With Supabase configured, authentication can be server-backed, but this repository does not include a CHAKRAVYUH reward-verification RPC/database schema; consequently, the simulator will not issue XP or credits in that mode. A secure cross-device leaderboard and authoritative rewards require a separately deployed server-side validation service. Supabase configuration alone does not provide that feature.

The leaderboard is intentionally identified as unavailable until such a service is deployed. Daily dates and streaks use UTC. Optional hints and cosmetic unlocks are demo credit purchases.

## Build and validation

```bash
npm run build
npm run lint
```
