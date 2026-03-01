# 🏛️ Samskritam Practice App — Architecture & Design

> High-level architecture, data flow, and trade-off decisions

---

## 1. System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                        CLIENT (Browser/PWA)                         │
│                                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌───────────────────┐  │
│  │  Next.js  │  │ Tailwind │  │  Zustand  │  │   Service Worker  │  │
│  │  App      │  │  CSS +   │  │  State    │  │   (Serwist/PWA)   │  │
│  │  Router   │  │  Indian  │  │  Mgmt     │  │   Offline Cache   │  │
│  └────┬─────┘  └──────────┘  └──────────┘  └───────────────────┘  │
│       │                                                             │
│  ┌────┴──────────────────────────────────────────────────────────┐  │
│  │              Exercise Component Registry                       │  │
│  │  ┌─────┐ ┌────────┐ ┌─────┐ ┌───────┐ ┌────────┐ ┌───────┐  │  │
│  │  │ MCQ │ │ WMatch │ │ FIB │ │ Linga │ │Vachana │ │Speech │  │  │
│  │  └─────┘ └────────┘ └─────┘ └───────┘ └────────┘ └───────┘  │  │
│  └───────────────────────────────────────────────────────────────┘  │
└─────────────────────────┬───────────────────────────────────────────┘
                          │ HTTPS (REST API)
                          ▼
┌─────────────────────────────────────────────────────────────────────┐
│                     API LAYER (Serverless)                           │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │              Next.js API Routes (on AWS Amplify)              │   │
│  │                                                              │   │
│  │  /api/auth/*        → Cognito session management             │   │
│  │  /api/exercises     → Exercise serving (GET)                 │   │
│  │  /api/attempts      → Record attempts (POST)                │   │
│  │  /api/sessions      → Session management (CRUD)             │   │
│  │  /api/scores        → Scoring & leaderboard (GET)           │   │
│  │  /api/curriculum    → Curriculum CRUD (teacher)             │   │
│  │  /api/classes       → Class management (teacher)            │   │
│  │  /api/students      → Student progress (teacher)            │   │
│  │  /api/health        → Health check endpoint                 │   │
│  └──────────────────────┬───────────────────────────────────────┘   │
│                         │                                           │
│  ┌──────────────────────┴───────────────────────────────────────┐   │
│  │                    Prisma ORM Layer                           │   │
│  │         Type-safe queries, migrations, seed scripts          │   │
│  └──────────────────────┬───────────────────────────────────────┘   │
└─────────────────────────┼───────────────────────────────────────────┘
                          │
          ┌───────────────┼───────────────────┐
          ▼               ▼                   ▼
┌──────────────┐ ┌──────────────┐  ┌──────────────────┐
│  AWS Cognito │ │  PostgreSQL  │  │     AWS S3       │
│              │ │  (AWS RDS)   │  │                  │
│ Google OAuth │ │              │  │ Avatar images    │
│ JWT tokens   │ │ Users        │  │ Audio files      │
│ User pools   │ │ Classes      │  │ Exercise assets  │
│ Groups       │ │ Curriculum   │  │                  │
│ (student/    │ │ Exercises    │  │                  │
│  teacher)    │ │ Progress     │  │                  │
│              │ │ Sessions     │  │                  │
│              │ │ Scores       │  │                  │
└──────────────┘ └──────────────┘  └──────────────────┘
```

---

## 2. Key Technology Decisions

| Category | Choice | Rationale |
|----------|--------|-----------|
| Framework | Next.js 14 (App Router) | SSR + API routes + PWA in one codebase, Amplify native support |
| Database | PostgreSQL (AWS RDS) | Relational fits curriculum hierarchy, Prisma support, 12-month free tier |
| Auth | AWS Cognito | 50K MAU free, Google OAuth built-in, user groups for roles |
| Hosting | AWS Amplify | Full-stack Next.js support, CI/CD from GitHub, ~$5-15/mo |
| State | Zustand | Tiny (1KB), simple API, right-sized for session/score state |
| ORM | Prisma | Type-safe, auto-migrations, schema-as-code, seed scripts |
| Drag & Drop | @dnd-kit | Best touch support, accessible, actively maintained |
| Speech | Web Speech API (MVP) → Whisper (P2) | Free for MVP, upgrade path to self-hosted Whisper |
| PWA | Serwist | Modern fork of next-pwa, App Router compatible |
| Project Mgmt | GitHub Projects | Free, integrated with repo, MCP-automatable |

---

## 3. Exercise Component Registry Pattern

New exercise types can be added without changing the core engine:

1. Create React component implementing `ExerciseProps` interface
2. Create validator function
3. Register in `ExerciseRegistry`
4. Add enum value via `prisma migrate`
5. Add exercises to seed data

---

## 4. Curriculum Data Model

```
Course → Module → Lesson → Exercise
```

Each exercise has: type, prompt (Devanagari), options, correctAnswer, difficulty, and extensible metadata JSON.

---

## 5. Scoring & Streak Logic

- Correct: streak++, points = 10 × multiplier
- Wrong: streak = 0, points = 0
- Multipliers: 1× (streak < 3), 2× (streak ≥ 3), 3× (streak ≥ 6)
- Session completion bonus: +50 points

---

## 6. Cost Optimization

| Phase | Monthly Cost |
|-------|--------------|
| Development (Month 1-2) | $0 (all free tier) |
| MVP Launch (Month 3) | ~$5-10 |
| Growth (Month 4-12) | ~$10-15 |
| Post Free Tier (Month 13+) | ~$25-30 |

Fallback: Migrate DB to Supabase free tier (PostgreSQL compatible) if costs spike.
