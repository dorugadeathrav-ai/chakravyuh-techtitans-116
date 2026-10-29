# ENTC InnovateHub

A modern smart learning platform for Electronics and Telecommunication Engineering students.

## Features

- Student dashboard with mission progress graph
- Login and registration using Supabase Auth when configured; development-only demo access otherwise
- Interactive ENTC learning modules
- Virtual electronics lab with Ohm’s law, logic gates, LED circuit, and streetlight simulators
- Rule-based AI learning assistant examples (no live model or AI backend is configured)
- Arduino coding challenges with safe rule-based validation
- Quiz Zone with 10-question random and daily challenges, post-submission answer review, and skill/topic feedback
- CHAKRAVYUH mission track with XP, credits, stars, levels, achievements, and cosmetic unlocks
- CHAKRAVYUH Circuit Lab with a searchable component library, pin-level wiring, dragging, rotation, zoom/pan, undo/redo, save/load, SVG diagram and CSV bill-of-materials export
- Books Library with search, subject/author/semester/difficulty filters, details, official publisher websites, bookmarks, and reading status
- Video Learning Hub with ENTC subject paths, YouTube playlist embeds/search, Watch Later, and student-confirmed lesson steps
- Components & Prices catalogue with project templates, Circuit Lab import, BOM estimates, budget checks, CSV export, and print
- Quiz Zone with 10-question random, daily, subject, topic, Arduino, troubleshooting, and learning-skills practice; answer review and skill feedback

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

## Video Learning Hub

The Video Learning Hub covers 16 ENTC subject areas with topic search fallbacks, two curated playlist links whose YouTube page titles were verified, and the supplied channel-playlists link as it resolves (Programming Electronics Academy). The supplied Digital Electronics playlist did not return a verifiable title and is not listed as curated. Search results are opened on YouTube; individual search videos, titles, channel metadata, and thumbnails are not invented or asserted as verified. The official YouTube IFrame Player API is loaded for the two verified playlist embeds. It requires no Data API key; playback may still be blocked by YouTube, browser privacy controls, or the video's embedding settings, in which case the original resource/search link remains available. No YouTube Data API or live video/playlist discovery is configured.

Watch Later entries, subject lesson steps, quiz links, and recent activity are stored in browser local storage under the signed-in email. Playlist watch completion is not reliably exposed, so the student confirms watching; practical activity is also student-confirmed. A path requires the watch confirmation, a concept reflection, a submitted 10-question quiz scoped to that path's available Quiz Zone subject, and practical confirmation. Demo mode awards 25 XP and 5 credits once per completed subject path. These client-side rewards are editable and are disabled when Supabase is configured because no trusted reward endpoint exists. Books and Circuit Lab links open those platform pages; recommendations are starter guidance rather than AI-generated or server-personalized results.

## Components & Prices

The searchable starter catalogue covers development boards, components, sensors, output devices, communications, lab tools, and project kits. Entries are product types, not verified SKU listings; product images are neutral placeholders, and there are no verified supplier prices, availability, ratings, purchase links, or price histories. Prices are left blank. Manually entered BOM amounts are labeled as student estimates and are not represented as market prices. Use a datasheet and supplier quote to confirm model compatibility and price.

Eight editable project templates are provided. Circuit Lab import maps only recognized component types, groups repeated parts, excludes ground symbols, leaves price blank, and reports unsupported mappings instead of guessing. Parts subtotal and contingency apply to priced items only; an estimate with unpriced parts is marked incomplete and budget fit is unknown. Shipping, tax, and contingency are separate user-configured values; check supplier quotes to avoid double counting. Estimates are saved in browser local storage by account email and can be loaded, exported as CSV, or printed (including print-to-PDF in the browser).

There is no database migration or shared catalogue/admin interface, product-image feed, supplier API, live price integration, authorized supplier lookup, price sorting, SKU-level compatibility checker, or native PDF/share service. The current component catalogue is static source data and changes require code updates. Only project estimates are user-editable, in this browser; no cross-device or server persistence is provided. Demo estimates must not be used as purchasing quotes.

In development/demo authentication mode, game progress is stored in this browser under the student's email, survives logout/login in that browser, and gives each mission rewards only once. This local progress is not tamper-resistant and must not be used for official grades, prizes, or competitive rankings. With Supabase configured, authentication can be server-backed, but this repository does not include a CHAKRAVYUH reward-verification RPC/database schema; consequently, the simulator will not issue XP or credits in that mode. A secure cross-device leaderboard and authoritative rewards require a separately deployed server-side validation service. Supabase configuration alone does not provide that feature.

The leaderboard is intentionally identified as unavailable until such a service is deployed. Daily dates and streaks use UTC. Optional hints and cosmetic unlocks are demo credit purchases.

## Quiz Zone

The Quiz Zone uses a curated, local bank of 30 ENTC multiple-choice questions mapped to subject, broad topic group, difficulty, and a learning skill. A session starts only when its selected filters match at least 10 questions; each valid session samples exactly 10 distinct questions. Random practice samples a shuffled mix, and the daily challenge is stable for the current UTC date. The bank includes subject and topic-group sets, 10 questions in each difficulty band across the full bank, book-aligned subject practice, Arduino questions, troubleshooting questions, and learning-skills practice. Combinations with fewer than 10 matching questions are disabled instead of silently padding a quiz with unrelated questions.

Answers and explanations remain hidden until submission. The quiz records selected answers, time, hints used, and a skill/topic breakdown; local results include accuracy history and recommendations for related catalogue subjects and Circuit Lab practice. These are deterministic rule-based recommendations, not AI-generated content. Question entries are included in the frontend bundle because there is no protected question-bank API, so this is a learning feature rather than a secure exam or assessment service.

Quiz attempts and question-level reviews are saved in browser local storage, scoped to the signed-in email. In development/demo authentication mode, a submitted attempt grants 50 XP, stars at 60/80/90 percent thresholds, and 10 demo credits for an Advanced quiz scored at least 80 percent. The app records rewarded attempt IDs to avoid duplicate reward callbacks. These client-side records can be edited by the browser user and are not authoritative. With Supabase authentication, quiz history remains local and rewards are disabled because no trusted scoring/reward endpoint is present. There is no admin question editor, AI question generator, server-side quiz persistence, or secure leaderboard.

## Build and validation

```bash
npm run build
npm run lint
```
