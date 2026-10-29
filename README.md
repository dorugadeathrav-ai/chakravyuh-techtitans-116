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

## Build and validation

```bash
npm run build
npm run lint
```

