# Braid Landing Page Design Spec

## Overview

Single-page marketing site for Braid — a desktop app that organizes parallel AI-assisted development workflows by linking tasks, terminals, and GitHub into one interface.

**Goal:** Sell Braid to developers doing parallel AI-powered work. Convert visitors to downloads with a freemium model (1 free project, $10/month for Pro).

**Target audience:** Solo developers juggling multiple AI sessions (entry point), small teams needing shared visibility (upgrade path).

## Tech Stack

- **Astro** — static site generator, zero JS by default
- **Tailwind CSS v4** — utility-first styling, matches the app's stack
- **Deployed as static HTML** — any CDN (Vercel, Netlify, Cloudflare Pages)
- **No client-side framework** — pure static, fast load

## Visual Design

### Color Palette (derived from logo)

| Token | Value | Usage |
|-------|-------|-------|
| `bg-base` | `#0A0A0F` | Page background |
| `bg-surface` | `#141419` | Card/section backgrounds |
| `bg-surface-raised` | `#1E1E26` | Elevated elements, hover states |
| `border-default` | `#2A2A35` | Card borders, dividers |
| `border-accent` | `#8B5CF6` | Accent borders (purple) |
| `text-primary` | `#F0F0F0` | Headings, primary text |
| `text-secondary` | `#9CA3AF` | Body text, descriptions |
| `text-muted` | `#6B7280` | Tertiary text, labels |
| `accent-purple` | `#8B5CF6` | Primary accent (from logo) |
| `accent-green` | `#4ADE80` | CTA buttons, success states |
| `accent-blue` | `#60A5FA` | Links, secondary accent |
| `fresh` | `#1D9E75` | Staleness indicator - fresh |
| `warm` | `#EF9F27` | Staleness indicator - warm |
| `stale` | `#E24B4A` | Staleness indicator - stale |

### Typography

- **Headings:** Inter (700, 600 weights)
- **Body:** Inter (400, 500 weights)
- **Code/terminal:** JetBrains Mono
- **Scale:** Hero h1 ~56px, section h2 ~40px, card h3 ~24px, body 16-18px

### Effects

- Subtle purple-to-green gradient on accent borders and highlights
- Soft glow behind hero screenshot (radial gradient, low opacity purple/green)
- Cards with subtle border, slight hover lift
- Smooth scroll between sections

## Page Structure

### Nav (sticky)

- Logo (Braid icon + wordmark) left-aligned
- Links: Features, Pricing (anchor links)
- CTA button: "Download" right-aligned
- Transparent background, gains bg-surface on scroll

### Section 1: Hero

- **Headline:** "Tame the chaos of parallel development"
- **Subheadline:** "Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together."
- **Primary CTA:** Green button — "Download for Mac" (links to download/release)
- **Secondary CTA:** Text link — "See pricing" (anchor to pricing section)
- **Visual:** App screenshot, centered, with perspective tilt and a subtle radial glow behind it. The screenshot is the hero — it shows the real product.

### Section 2: Problem Statement

Three cards in a horizontal row (stacks on mobile):

1. **Icon:** Terminal icon
   **Heading:** "5 terminals, 3 branches, zero context"
   **Body:** "You're juggling Claude sessions, feature branches, and PR reviews. Which terminal was for which task?"

2. **Icon:** Refresh/switch icon
   **Heading:** "Context switching is killing your flow"
   **Body:** "Every time you swap tasks, you lose minutes rebuilding mental state. Multiply that by a full day of AI-assisted work."

3. **Icon:** Puzzle/disconnect icon
   **Heading:** "Your tools don't know about each other"
   **Body:** "GitHub in one tab, terminal in another, notes in a third. Nothing is connected."

### Section 3: Feature Showcase

Four feature blocks, alternating image/text layout:

**Feature 1: Task-linked terminals**
- Heading: "One task, one terminal, one place"
- Body: "Create a task, spawn a terminal. Every command, every output, linked to the work it belongs to. Switch tasks instantly with the cockpit bar."
- Visual: Cropped screenshot highlighting the task sidebar + terminal + cockpit bar

**Feature 2: Staleness tracking**
- Heading: "Staleness at a glance"
- Body: "Color-coded indicators show which tasks are fresh, warming, or going stale. Never lose track of a thread again."
- Visual: Illustration or cropped screenshot showing green/orange/red dots next to tasks

**Feature 3: Git worktrees**
- Heading: "Git worktrees, automatically"
- Body: "Each task gets its own isolated branch and worktree. No more stashing, no more 'which branch am I on?' Braid handles it."
- Visual: Stylized terminal showing branch isolation

**Feature 4: GitHub integration**
- Heading: "GitHub in your workflow"
- Body: "Link PRs to tasks. Get notifications, CI status, and review requests right where you're working."
- Visual: Cropped screenshot or illustration of GitHub PR linked to a task

### Section 4: Team Features

Single centered block with a wider card:

- **Heading:** "See what your team is working on"
- **Body:** "Real-time presence shows who's active, idle, or offline — and which task they're on. Shared workspace, shared visibility. No standups needed to know what's in flight."
- **Visual:** Stylized presence indicators with avatar placeholders

### Section 5: Pricing

Two cards side by side (stacks on mobile):

**Free card:**
- Heading: "Free"
- Price: "$0"
- Features list:
  - 1 project
  - Unlimited tasks
  - Unlimited terminals
  - GitHub integration
  - Git worktree isolation
- CTA: "Download for free"

**Pro card (highlighted):**
- Badge: "Most popular"
- Heading: "Pro"
- Price: "$10/month"
- Features list:
  - Everything in Free
  - Unlimited projects
  - Team workspaces
  - Real-time collaboration
  - Priority support
- CTA: "Start free trial"
- Green border accent, slightly elevated

### Section 6: Final CTA

- **Heading:** "Stop juggling. Start braiding."
- **CTA:** Green download button
- **Subtext:** "Available for macOS. Windows & Linux coming soon."

### Section 7: Footer

- Logo (small)
- Copyright: "2026 Braid"
- Links: GitHub, Twitter/X, Contact
- Minimal, single row

## Responsive Behavior

- **Desktop (1024px+):** Full layout as described, max-width ~1200px centered
- **Tablet (768-1023px):** Feature blocks stack vertically, pricing cards stay side by side
- **Mobile (<768px):** Everything stacks, hero headline shrinks to ~36px, nav collapses to hamburger or simplified

## Assets Required

- Braid logo (PNG/SVG — already have the icon)
- App screenshot (already have)
- Cropped feature screenshots (can be created from the full screenshot or generated as stylized illustrations using CSS)

## File Structure

```
braid.software/
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # Base HTML layout
│   ├── pages/
│   │   └── index.astro           # Landing page
│   ├── components/
│   │   ├── Nav.astro
│   │   ├── Hero.astro
│   │   ├── ProblemStatement.astro
│   │   ├── Features.astro
│   │   ├── TeamFeatures.astro
│   │   ├── Pricing.astro
│   │   ├── FinalCTA.astro
│   │   └── Footer.astro
│   └── styles/
│       └── global.css            # Tailwind imports + custom properties
├── public/
│   ├── braid-logo.png            # Logo asset
│   ├── app-screenshot.png        # Hero screenshot
│   └── favicon.ico
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Out of Scope

- Blog / changelog pages
- Documentation
- Authentication / account management on the marketing site
- Analytics (can be added later)
- Download infrastructure (CTA links to GitHub releases or external download for now)
