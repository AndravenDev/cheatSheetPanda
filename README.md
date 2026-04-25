# CheatSheet Panda

A developer cheat-sheet platform built with **Nuxt 4**, **Tailwind CSS v4**, and **@nuxt/icon** (Iconify).

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Nuxt 4 |
| UI | Vue 3 (Composition API, `<script setup>`) |
| Styles | Tailwind CSS v4 (Vite plugin, CSS-first config) |
| Icons | @nuxt/icon + simple-icons + lucide |
| Font | Inter (Google Fonts via `<head>` link) |
| Language | TypeScript |

---

## Getting Started

### Prerequisites

- Node.js `>= 18`
- npm

### Install

```bash
npm install
```

### Dev server

```bash
npm run dev
# → http://localhost:3000
```

### Production build

```bash
npm run build
npm run preview
```

### Static site

```bash
npm run generate
```

---

## Project Structure

```
cheatSheetPanda/
├── app/
│   ├── assets/css/main.css      # Tailwind v4 CSS-first config (@theme, @keyframes)
│   ├── components/
│   │   ├── AppHeader.vue        # Fixed nav — logo, links, CTA, scroll-aware bg
│   │   ├── HeroSection.vue      # Full hero — floating cards, search bar, pills
│   │   └── FloatingCard.vue     # Reusable glassmorphism tech card
│   ├── pages/
│   │   └── index.vue            # Landing page entry point
│   └── app.vue                  # Root (renders <NuxtPage />)
├── public/                      # Static assets (favicon, robots.txt)
├── nuxt.config.ts               # Nuxt + Tailwind Vite plugin config
└── package.json
```

---

## Placeholder Images

Two images are referenced but not yet provided. Drop them into `public/` when ready:

| File | Used in | Notes |
|---|---|---|
| `/panda-logo.png` | `AppHeader.vue` | 32 × 32 px circular logo; currently shows 🐼 emoji |
| `/panda-hero.png` | `HeroSection.vue` | Large hero illustration; currently shows 🐼 emoji |

To swap in the images, replace the placeholder `<div>` elements marked with the comment `<!-- PLACEHOLDER -->` in each component.

---

## Custom Tailwind Theme

Defined in `app/assets/css/main.css` via Tailwind v4's `@theme` block:

| Token | Value |
|---|---|
| `navy-deep` | `#0a1628` |
| `navy-mid` | `#0f1f3d` |
| `navy-light` | `#1a2f52` |
| `mint` | `#4ade80` |
| `teal-glow` | `#2dd4bf` |
| `animate-float` | 6 s ease-in-out infinite float |

---

## Adding New Pages / Sections

Follow Nuxt's file-based routing — add `app/pages/about.vue`, etc. Components in `app/components/` are auto-imported.

---

## License

MIT
