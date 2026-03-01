# 📋 Samskritam Practice App — Project Status

> Last updated: March 1, 2026

---

## 🏠 Project Links

| Resource | Link |
|----------|------|
| **GitHub Repo** | https://github.com/paninij-zz/samskritam-app |
| **Project Board** | https://github.com/users/paninij-zz/projects/1 |
| **Spec Document** | `SPEC.md` |
| **Curriculum** | `CURRICULUM.md` |
| **Architecture** | `ARCHITECTURE.md` |

---

## ✅ What's Been Completed

### Infrastructure
- [x] GitHub MCP Server installed locally (v0.31.0, pre-built binary)
- [x] GitHub repository created: `paninij-zz/samskritam-app`
- [x] GitHub Project board created: "Learn Samskritam App" (Project #1)
- [x] Classic PAT configured with `repo` + `project` scopes

### Planning & Organization
- [x] Product Specification written (`SPEC.md`) — 48 user stories across 10 themes
- [x] Curriculum structured (`CURRICULUM.md`) — 37 modules, ~55 lessons, 6 exercise types
- [x] Architecture documented (`ARCHITECTURE.md`) — diagrams, data flow, trade-offs
- [x] 9 Epics created and added to project board
- [x] 28 task issues created covering all P0, key P1, and key P2 stories
- [x] All 37 issues added to "Learn Samskritam App" project board

### UX Research & Prototyping
- [x] Researched Duolingo, Babbel, Drops UX patterns
- [x] Extracted content from teacher's Lesson 1.1 slides (भवतः नाम, भवत्याः नाम, मम नाम)
- [x] **V1 Prototype** (`prototype/index.html`) — Clean exercise-focused UI
  - 10 screens: Invocation → Lesson Intro → Listen → MCQ × 2 → Tap Pairs → Sentence Builder → Fill-in-Blank → Gender Awareness → Summary
  - Indianized color palette (saffron, turmeric, sindoor, forest green)
  - Noto Sans Devanagari fonts, sound effects, confetti, streak scoring
- [x] **V2 Prototype** (`prototype/v2-dialogue.html`) — Dialogue + Characters
  - Characters interact with speech bubbles (like teacher's slides)
  - Character emotions: 😄 bounce on correct, 😔 shake on wrong
  - Rotating Puranic guru reactions (रामः, व्यासः, शिवः, लक्ष्मी, सरस्वती, कृष्णः)
  - Confetti only on streak ≥ 5
  - Dialogue-based exercises: "Help सुरेशः reply!", "Fill in माया's speech bubble"

### Feedback Received on V2 (→ V3 Plan)
1. **Characters**: Current emoji chars OK but need proper illustrated character pack → **OpenPeeps (CC0)** SVG characters
2. **Guru panel**: Bottom panel with Lakshmi/Vyasa/Rama is overkill → Replace with simple floating emoji reaction
3. **Streak animations**: Tiered system — Sanskrit text bursts ("साधु!", "उत्तमम्!", "अद्भुतम्!") only at milestones (5, 10, 15), confetti resets every 5
4. **Score HUD**: Show score top-left, streak as 5-star meter top-right
5. **Modern web trends**: Glassmorphism, micro-interactions, View Transitions API, container queries
6. **Character pack decision**: OpenPeeps (CC0, no attribution) for student/teacher SVG characters

---

## 🎨 Character Pack Decision

| Pack | License | Style | Decision |
|------|---------|-------|----------|
| **OpenPeeps** | CC0 (free forever) | Hand-drawn, diverse, modular SVG | ✅ **CHOSEN** |
| Avataaars | MIT | Cartoon, customizable | Backup option |
| Humaaans | CC0 | Mix-and-match | For scene illustrations |

---

## 📊 Epic Summary

| # | Epic | Issue | Priority | Sprint | Status |
|---|------|-------|----------|--------|--------|
| 1 | 🏗️ Foundation & DevOps | [#4](https://github.com/paninij-zz/samskritam-app/issues/4) | P0 | Sprint 1 | 📋 Backlog |
| 2 | 🔐 Auth & Onboarding | [#5](https://github.com/paninij-zz/samskritam-app/issues/5) | P0 | Sprint 1 | 📋 Backlog |
| 3 | 🎮 Core Practice Engine | [#6](https://github.com/paninij-zz/samskritam-app/issues/6) | P0 | Sprint 2 | 📋 Backlog |
| 4 | 📚 Curriculum & Content Pipeline | [#7](https://github.com/paninij-zz/samskritam-app/issues/7) | P0-P1 | Sprint 2-4 | 📋 Backlog |
| 5 | 🏆 Social & Gamification | [#8](https://github.com/paninij-zz/samskritam-app/issues/8) | P1 | Sprint 3 | 📋 Backlog |
| 6 | 📊 Teacher Dashboard & Analytics | [#9](https://github.com/paninij-zz/samskritam-app/issues/9) | P1 | Sprint 3 | 📋 Backlog |
| 7 | 🎨 Polish & Engagement | [#10](https://github.com/paninij-zz/samskritam-app/issues/10) | P1-P2 | Sprint 4 | 📋 Backlog |
| 8 | 🎤 Speech & Pronunciation | [#11](https://github.com/paninij-zz/samskritam-app/issues/11) | P2 | Sprint 4+ | 📋 Backlog |
| 9 | 📦 Offline, Notifications & Reliability | [#12](https://github.com/paninij-zz/samskritam-app/issues/12) | P2 | Sprint 4+ | 📋 Backlog |

---

## 🗓️ Sprint Plan

| Sprint | Weeks | Focus | Epics |
|--------|-------|-------|-------|
| **Sprint 1** | Week 1-2 | Foundation + Auth + Onboarding | Epic 1, Epic 2 |
| **Sprint 2** | Week 3-4 | Core Practice Engine + Seed Data | Epic 3, Epic 4 (start) |
| **Sprint 3** | Week 5-6 | Social + Teacher Dashboard | Epic 5, Epic 6, Epic 4 (continue) |
| **Sprint 4** | Week 7-8 | Polish + Speech + Offline | Epic 7, Epic 8, Epic 9 |

---

## 🚀 How to Pick Up

1. Open this project in Kiro
2. The GitHub MCP Server is already configured and running
3. Check the project board: https://github.com/users/paninij-zz/projects/1
4. Start with **Epic 1** (Foundation) — Issue #4
5. Reference `ARCHITECTURE.md` for design decisions
6. Reference `CURRICULUM.md` for exercise content
7. Reference `SPEC.md` for detailed requirements
8. See `prototype/` folder for UX prototypes (V1, V2, V3)
