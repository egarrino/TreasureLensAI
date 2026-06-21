# TreasureLens AI

**Scan a room. Discover what it's worth.**

Take one photo of a room and TreasureLens AI detects every item, appraises it,
drafts marketplace-ready listings, builds a sell / bundle / donate plan, and
negotiates with buyers — you just approve and get paid.

This repository is the front-end demo: a fast, deterministic walkthrough of that
experience across five room types.

## Demo

- **Live demo** — https://treasurelens-ai.netlify.app/
- **Video walkthrough** — https://youtu.be/r6d-lIeVIZg
- **Event** — UC Berkeley AI Hackathon 2026

## Quick start

First time only, install dependencies:

```bash
pnpm install
```

### Windows

```powershell
.\Start-Estatescan.ps1
```

Then open the printed URL (defaults to http://localhost:5173/). Pass
`-Port 5180` to use a different port.

### Any platform

```bash
pnpm --filter @workspace/estatescan run dev
```

The dev server listens on `PORT` / `BASE_PATH` if set, and otherwise defaults to
`5173` and `/`.

## Useful scripts

- `pnpm --filter @workspace/estatescan run dev` — run the TreasureLens app
- `pnpm --filter @workspace/estatescan run typecheck` — typecheck the app
- `pnpm run typecheck` — typecheck every package
- `pnpm run build` — typecheck + build every package

## Stack

- pnpm workspaces · Node.js 24 · TypeScript 5.9
- React + Vite (app lives in `artifacts/estatescan`)
- Routing: wouter · Animation: framer-motion
- UI: shadcn-style components + Tailwind CSS

## How it works

The product is modeled as five model-agnostic stages with typed contracts, so a
live vision model and a real comps source can drop in behind the same interfaces
the demo already runs on:

1. **Vision** — detect each item, brand, condition, confidence, and location
2. **Valuation** — price range + confidence (`value = base × brand × condition × demand × completeness`)
3. **Recommendation** — Sell / Bundle / Appraise / Donate / Recycle / Keep
4. **Listing** — marketplace-ready title, description, and pricing
5. **Negotiation** — evaluate a buyer offer: accept / counter / decline

A human-approval gate sits on every listing and every offer — the agent
recommends, the person decides.

## Project layout

- `artifacts/estatescan/src/pages/Landing.tsx` — room picker / hero
- `artifacts/estatescan/src/pages/ScanAnimation.tsx` — scripted scan with a climbing value counter
- `artifacts/estatescan/src/pages/Dashboard.tsx` — detected items, hidden treasures, plan, listings, negotiation copilot
- `artifacts/estatescan/src/lib/data.ts` — all scripted demo data (rooms, items, value checkpoints)
- `artifacts/estatescan/public/` — item and room images referenced from `data.ts`

Routes: `/` (Landing) → `/scan` (ScanAnimation) → `/dashboard` (Dashboard).

## Notes

- Front-end only by design: no backend, auth, or database. Every value and "AI"
  response is scripted client-side for a deterministic, reliable demo.
- Each `imageUrl` in `data.ts` must resolve to a file in
  `artifacts/estatescan/public/`, or the dashboard shows a broken image.

---

*© 2026 Enrica Garrino. TreasureLens AI — original concept, design, and source code. All rights reserved.*# TreasureLensAI
