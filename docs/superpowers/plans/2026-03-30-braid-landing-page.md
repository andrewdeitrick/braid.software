# Braid Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page marketing site for Braid that sells the product and converts developers to downloads, with a freemium pricing model.

**Architecture:** Static Astro site with Tailwind CSS v4. One `index.astro` page composed of Astro components for each section (Nav, Hero, Problem, Features, Team, Pricing, CTA, Footer). Ships zero JavaScript — pure HTML+CSS. Dark theme matching the app's aesthetic.

**Tech Stack:** Astro 5, Tailwind CSS v4 (via `@tailwindcss/vite`), Inter + JetBrains Mono fonts from Google Fonts / Fontsource

---

## File Structure

```
braid.software/
├── src/
│   ├── layouts/
│   │   └── Layout.astro            # <html> shell: head, meta, fonts, body wrapper
│   ├── pages/
│   │   └── index.astro             # Imports and composes all section components
│   ├── components/
│   │   ├── Nav.astro               # Sticky nav: logo, anchor links, download CTA
│   │   ├── Hero.astro              # Headline, subheadline, CTAs, screenshot with glow
│   │   ├── ProblemStatement.astro  # Three pain-point cards
│   │   ├── Features.astro          # Four alternating feature blocks
│   │   ├── TeamFeatures.astro      # Single centered team card
│   │   ├── Pricing.astro           # Free + Pro pricing cards
│   │   ├── FinalCTA.astro          # Closing headline + download button
│   │   └── Footer.astro            # Logo, copyright, links
│   └── styles/
│       └── global.css              # Tailwind v4 imports + custom theme tokens
├── public/
│   ├── braid-logo.png              # App icon (copied from user's file)
│   ├── app-screenshot.png          # App screenshot (copied from user's file)
│   └── favicon.png                 # Favicon (use logo)
├── astro.config.mjs                # Astro config with Tailwind vite plugin
├── package.json
└── tsconfig.json
```

---

### Task 1: Scaffold Astro Project with Tailwind

**Files:**
- Create: `package.json`
- Create: `astro.config.mjs`
- Create: `tsconfig.json`
- Create: `src/styles/global.css`
- Create: `src/layouts/Layout.astro`
- Create: `src/pages/index.astro`

- [ ] **Step 1: Initialize the Astro project**

Run:
```bash
cd /Users/andrewdeitrick/workspace/braid.software
npm create astro@latest . -- --template minimal --no-install --no-git --typescript strict
```

Expected: Astro scaffolds minimal files into current directory.

- [ ] **Step 2: Install dependencies**

Run:
```bash
cd /Users/andrewdeitrick/workspace/braid.software
npm install
npm install -D @tailwindcss/vite tailwindcss
```

Expected: node_modules populated, package-lock.json created.

- [ ] **Step 3: Configure Astro to use Tailwind via Vite plugin**

Write `astro.config.mjs`:

```javascript
import { defineConfig } from "astro/config";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  vite: {
    plugins: [tailwindcss()],
  },
});
```

- [ ] **Step 4: Create global.css with Tailwind v4 imports and custom theme**

Write `src/styles/global.css`:

```css
@import "tailwindcss";

@theme {
  --color-bg-base: #0A0A0F;
  --color-bg-surface: #141419;
  --color-bg-surface-raised: #1E1E26;
  --color-border-default: #2A2A35;
  --color-border-accent: #8B5CF6;
  --color-text-primary: #F0F0F0;
  --color-text-secondary: #9CA3AF;
  --color-text-muted: #6B7280;
  --color-accent-purple: #8B5CF6;
  --color-accent-green: #4ADE80;
  --color-accent-blue: #60A5FA;
  --color-fresh: #1D9E75;
  --color-warm: #EF9F27;
  --color-stale: #E24B4A;
  --font-sans: "Inter", ui-sans-serif, system-ui, sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, monospace;
}

html {
  scroll-behavior: smooth;
}

body {
  background-color: var(--color-bg-base);
  color: var(--color-text-primary);
  font-family: var(--font-sans);
}
```

- [ ] **Step 5: Create the base Layout.astro**

Write `src/layouts/Layout.astro`:

```astro
---
interface Props {
  title: string;
  description: string;
}
const { title, description } = Astro.props;
---

<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content={description} />
    <title>{title}</title>
    <link rel="icon" type="image/png" href="/favicon.png" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="/src/styles/global.css" />
  </head>
  <body class="antialiased">
    <slot />
  </body>
</html>
```

- [ ] **Step 6: Create a placeholder index.astro**

Write `src/pages/index.astro`:

```astro
---
import Layout from "../layouts/Layout.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <main>
    <h1 class="text-4xl font-bold text-text-primary text-center pt-40">Braid</h1>
    <p class="text-text-secondary text-center mt-4">Landing page coming together...</p>
  </main>
</Layout>
```

- [ ] **Step 7: Verify the dev server runs**

Run:
```bash
cd /Users/andrewdeitrick/workspace/braid.software
npx astro dev
```

Expected: Server starts on `localhost:4321`, page renders with "Braid" heading on dark background.

- [ ] **Step 8: Commit**

```bash
git add package.json package-lock.json astro.config.mjs tsconfig.json src/ public/
git commit -m "feat: scaffold Astro project with Tailwind v4"
```

---

### Task 2: Copy Assets and Create .gitignore

**Files:**
- Create: `public/braid-logo.png`
- Create: `public/app-screenshot.png`
- Create: `public/favicon.png`
- Create: `.gitignore`

- [ ] **Step 1: Copy the logo into public/**

Run:
```bash
cp /Users/andrewdeitrick/Downloads/braid.png /Users/andrewdeitrick/workspace/braid.software/public/braid-logo.png
```

- [ ] **Step 2: Copy the app screenshot into public/**

Run:
```bash
cp "/var/folders/s5/b6l8r_hd7z13p3tk2_6qqbfc0000gn/T/TemporaryItems/NSIRD_screencaptureui_g8WAwv/Screenshot 2026-03-30 at 10.27.55 AM.png" /Users/andrewdeitrick/workspace/braid.software/public/app-screenshot.png
```

- [ ] **Step 3: Copy the logo as favicon**

Run:
```bash
cp /Users/andrewdeitrick/Downloads/braid.png /Users/andrewdeitrick/workspace/braid.software/public/favicon.png
```

- [ ] **Step 4: Create .gitignore**

Write `.gitignore`:

```
node_modules/
dist/
.astro/
.DS_Store
```

- [ ] **Step 5: Commit**

```bash
git add public/ .gitignore
git commit -m "feat: add logo, screenshot, and favicon assets"
```

---

### Task 3: Nav Component

**Files:**
- Create: `src/components/Nav.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the Nav component**

Write `src/components/Nav.astro`:

```astro
<nav id="nav" class="fixed top-0 left-0 right-0 z-50 transition-colors duration-300">
  <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
    <a href="/" class="flex items-center gap-3">
      <img src="/braid-logo.png" alt="Braid" class="w-8 h-8 rounded-lg" />
      <span class="text-lg font-semibold text-text-primary">Braid</span>
    </a>
    <div class="hidden sm:flex items-center gap-8">
      <a href="#features" class="text-sm text-text-secondary hover:text-text-primary transition-colors">Features</a>
      <a href="#pricing" class="text-sm text-text-secondary hover:text-text-primary transition-colors">Pricing</a>
      <a href="#download" class="inline-flex items-center px-4 py-2 rounded-lg bg-accent-green text-bg-base text-sm font-semibold hover:brightness-110 transition">Download</a>
    </div>
  </div>
</nav>

<script>
  const nav = document.getElementById("nav");
  window.addEventListener("scroll", () => {
    if (window.scrollY > 20) {
      nav.classList.add("bg-bg-surface/95", "backdrop-blur-md", "border-b", "border-border-default");
    } else {
      nav.classList.remove("bg-bg-surface/95", "backdrop-blur-md", "border-b", "border-border-default");
    }
  });
</script>
```

- [ ] **Step 2: Add Nav to index.astro**

Replace the contents of `src/pages/index.astro`:

```astro
---
import Layout from "../layouts/Layout.astro";
import Nav from "../components/Nav.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <Nav />
  <main>
    <div class="pt-40 text-center">
      <h1 class="text-4xl font-bold">Braid</h1>
    </div>
  </main>
</Layout>
```

- [ ] **Step 3: Verify nav renders and scroll effect works**

Run: `npx astro dev` and check `localhost:4321`

Expected: Transparent nav at top, gains dark background with blur on scroll.

- [ ] **Step 4: Commit**

```bash
git add src/components/Nav.astro src/pages/index.astro
git commit -m "feat: add sticky nav with scroll background effect"
```

---

### Task 4: Hero Section

**Files:**
- Create: `src/components/Hero.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the Hero component**

Write `src/components/Hero.astro`:

```astro
<section class="relative pt-32 pb-20 px-6 overflow-hidden">
  <!-- Background glow -->
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[600px] rounded-full bg-accent-purple/10 blur-[120px] pointer-events-none"></div>
  <div class="absolute top-1/2 left-1/3 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[400px] rounded-full bg-accent-green/8 blur-[100px] pointer-events-none"></div>

  <div class="relative max-w-4xl mx-auto text-center">
    <h1 class="text-5xl sm:text-6xl lg:text-7xl font-bold tracking-tight leading-[1.1]">
      Tame the chaos of<br />
      <span class="bg-gradient-to-r from-accent-purple via-accent-blue to-accent-green bg-clip-text text-transparent">parallel development</span>
    </h1>

    <p class="mt-6 text-lg sm:text-xl text-text-secondary max-w-2xl mx-auto leading-relaxed">
      Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.
    </p>

    <div class="mt-10 flex flex-col sm:flex-row items-center justify-center gap-4">
      <a href="#download" class="inline-flex items-center px-8 py-3.5 rounded-xl bg-accent-green text-bg-base font-semibold text-base hover:brightness-110 transition shadow-lg shadow-accent-green/20">
        Download for Mac
      </a>
      <a href="#pricing" class="text-text-secondary hover:text-text-primary transition-colors text-sm">
        See pricing &darr;
      </a>
    </div>
  </div>

  <!-- App screenshot -->
  <div class="relative mt-20 max-w-5xl mx-auto">
    <div class="absolute inset-0 bg-gradient-to-t from-bg-base via-transparent to-transparent z-10 pointer-events-none"></div>
    <div class="rounded-xl overflow-hidden border border-border-default shadow-2xl shadow-accent-purple/10">
      <img
        src="/app-screenshot.png"
        alt="Braid application showing task management with integrated terminals"
        class="w-full"
        loading="eager"
      />
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add Hero to index.astro**

Replace `src/pages/index.astro`:

```astro
---
import Layout from "../layouts/Layout.astro";
import Nav from "../components/Nav.astro";
import Hero from "../components/Hero.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <Nav />
  <main>
    <Hero />
  </main>
</Layout>
```

- [ ] **Step 3: Verify hero renders with glow, gradient text, and screenshot**

Run dev server and check. Expected: Large headline with purple-to-green gradient on "parallel development", screenshot below with border and shadow, subtle glow behind both.

- [ ] **Step 4: Commit**

```bash
git add src/components/Hero.astro src/pages/index.astro
git commit -m "feat: add hero section with gradient headline and screenshot"
```

---

### Task 5: Problem Statement Section

**Files:**
- Create: `src/components/ProblemStatement.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the ProblemStatement component**

Write `src/components/ProblemStatement.astro`:

```astro
<section class="py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-3xl sm:text-4xl font-bold text-center mb-16">Sound familiar?</h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <!-- Card 1 -->
      <div class="rounded-xl border border-border-default bg-bg-surface p-8 hover:border-border-accent/40 transition-colors">
        <div class="w-10 h-10 rounded-lg bg-accent-purple/10 flex items-center justify-center mb-5">
          <svg class="w-5 h-5 text-accent-purple" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold mb-3">5 terminals, 3 branches, zero context</h3>
        <p class="text-text-secondary text-sm leading-relaxed">You're juggling Claude sessions, feature branches, and PR reviews. Which terminal was for which task?</p>
      </div>

      <!-- Card 2 -->
      <div class="rounded-xl border border-border-default bg-bg-surface p-8 hover:border-border-accent/40 transition-colors">
        <div class="w-10 h-10 rounded-lg bg-accent-blue/10 flex items-center justify-center mb-5">
          <svg class="w-5 h-5 text-accent-blue" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold mb-3">Context switching is killing your flow</h3>
        <p class="text-text-secondary text-sm leading-relaxed">Every time you swap tasks, you lose minutes rebuilding mental state. Multiply that by a full day of AI-assisted work.</p>
      </div>

      <!-- Card 3 -->
      <div class="rounded-xl border border-border-default bg-bg-surface p-8 hover:border-border-accent/40 transition-colors">
        <div class="w-10 h-10 rounded-lg bg-accent-green/10 flex items-center justify-center mb-5">
          <svg class="w-5 h-5 text-accent-green" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M11 4a2 2 0 114 0v1a1 1 0 001 1h3a1 1 0 011 1v3a1 1 0 01-1 1h-1a2 2 0 100 4h1a1 1 0 011 1v3a1 1 0 01-1 1h-3a1 1 0 01-1-1v-1a2 2 0 10-4 0v1a1 1 0 01-1 1H7a1 1 0 01-1-1v-3a1 1 0 00-1-1H4a2 2 0 110-4h1a1 1 0 001-1V7a1 1 0 011-1h3a1 1 0 001-1V4z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold mb-3">Your tools don't know about each other</h3>
        <p class="text-text-secondary text-sm leading-relaxed">GitHub in one tab, terminal in another, notes in a third. Nothing is connected.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add ProblemStatement to index.astro**

Add import and component after `<Hero />`:

```astro
---
import Layout from "../layouts/Layout.astro";
import Nav from "../components/Nav.astro";
import Hero from "../components/Hero.astro";
import ProblemStatement from "../components/ProblemStatement.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <Nav />
  <main>
    <Hero />
    <ProblemStatement />
  </main>
</Layout>
```

- [ ] **Step 3: Verify three cards render in a row (desktop) and stack (mobile)**

Expected: Three cards with icons, subtle hover border effect, responsive grid.

- [ ] **Step 4: Commit**

```bash
git add src/components/ProblemStatement.astro src/pages/index.astro
git commit -m "feat: add problem statement section with three pain-point cards"
```

---

### Task 6: Features Section

**Files:**
- Create: `src/components/Features.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the Features component**

Write `src/components/Features.astro`:

```astro
<section id="features" class="py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-3xl sm:text-4xl font-bold text-center mb-6">Everything in one place</h2>
    <p class="text-text-secondary text-center max-w-2xl mx-auto mb-20">Braid connects the tools you already use into a single workflow — so you can focus on building, not juggling.</p>

    <div class="space-y-24">
      <!-- Feature 1: Task-linked terminals -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div>
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-accent-purple/10 text-accent-purple text-xs font-medium mb-4">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
            </svg>
            Terminals
          </div>
          <h3 class="text-2xl sm:text-3xl font-bold mb-4">One task, one terminal, one place</h3>
          <p class="text-text-secondary leading-relaxed">Create a task, spawn a terminal. Every command, every output, linked to the work it belongs to. Switch tasks instantly with the cockpit bar at the bottom of your screen.</p>
        </div>
        <div class="rounded-xl border border-border-default bg-bg-surface p-4">
          <div class="rounded-lg bg-bg-base font-mono text-sm p-5 text-text-secondary">
            <p><span class="text-accent-green">$</span> <span class="text-text-primary">git checkout -b feat/auth-flow</span></p>
            <p class="text-text-muted">Switched to a new branch 'feat/auth-flow'</p>
            <p class="mt-2"><span class="text-accent-green">$</span> <span class="text-text-primary">npm run test -- --watch</span></p>
            <p class="text-fresh">PASS</p>
            <p class="mt-2"><span class="text-accent-green">$</span> <span class="text-text-primary">claude "implement OAuth flow"</span></p>
            <p class="text-accent-purple">Creating files...</p>
            <p class="mt-3 text-text-muted">─── <span class="text-fresh">Task: Auth Flow</span> · <span class="text-text-muted">shell 1</span> ───</p>
          </div>
        </div>
      </div>

      <!-- Feature 2: Staleness tracking -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="order-2 lg:order-1 rounded-xl border border-border-default bg-bg-surface p-6">
          <div class="space-y-3">
            <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base">
              <div class="w-2.5 h-2.5 rounded-full bg-fresh"></div>
              <span class="text-sm font-medium">Auth flow refactor</span>
              <span class="text-xs text-text-muted ml-auto">2m ago</span>
            </div>
            <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base">
              <div class="w-2.5 h-2.5 rounded-full bg-warm"></div>
              <span class="text-sm font-medium">Fix CI pipeline</span>
              <span class="text-xs text-text-muted ml-auto">4h ago</span>
            </div>
            <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base">
              <div class="w-2.5 h-2.5 rounded-full bg-stale"></div>
              <span class="text-sm font-medium">Update API docs</span>
              <span class="text-xs text-text-muted ml-auto">2d ago</span>
            </div>
            <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base">
              <div class="w-2.5 h-2.5 rounded-full bg-text-muted"></div>
              <span class="text-sm font-medium text-text-muted">Deploy script cleanup</span>
              <span class="text-xs text-text-muted ml-auto">parked</span>
            </div>
          </div>
        </div>
        <div class="order-1 lg:order-2">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-fresh/10 text-fresh text-xs font-medium mb-4">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
            </svg>
            Awareness
          </div>
          <h3 class="text-2xl sm:text-3xl font-bold mb-4">Staleness at a glance</h3>
          <p class="text-text-secondary leading-relaxed">Color-coded indicators show which tasks are fresh, warming, or going stale. Never lose track of a thread again — the tasks that need attention find you.</p>
        </div>
      </div>

      <!-- Feature 3: Git worktrees -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div>
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-accent-blue/10 text-accent-blue text-xs font-medium mb-4">
            <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zm10 0a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zm10 0a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
            </svg>
            Isolation
          </div>
          <h3 class="text-2xl sm:text-3xl font-bold mb-4">Git worktrees, automatically</h3>
          <p class="text-text-secondary leading-relaxed">Each task gets its own isolated branch and worktree. No more stashing, no more "which branch am I on?" Braid handles it.</p>
        </div>
        <div class="rounded-xl border border-border-default bg-bg-surface p-4">
          <div class="rounded-lg bg-bg-base font-mono text-sm p-5 text-text-secondary">
            <p class="text-text-muted"># Task: "Auth Flow" → auto-created worktree</p>
            <p><span class="text-accent-green">$</span> <span class="text-text-primary">pwd</span></p>
            <p>/projects/myapp<span class="text-accent-blue">/.worktrees/auth-flow</span></p>
            <p class="mt-2"><span class="text-accent-green">$</span> <span class="text-text-primary">git branch</span></p>
            <p>* <span class="text-fresh">feat/auth-flow</span></p>
            <p class="mt-3 text-text-muted"># Task: "Fix CI" → separate worktree</p>
            <p><span class="text-accent-green">$</span> <span class="text-text-primary">pwd</span></p>
            <p>/projects/myapp<span class="text-accent-blue">/.worktrees/fix-ci</span></p>
            <p><span class="text-accent-green">$</span> <span class="text-text-primary">git branch</span></p>
            <p>* <span class="text-warm">fix/ci-pipeline</span></p>
          </div>
        </div>
      </div>

      <!-- Feature 4: GitHub integration -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="order-2 lg:order-1 rounded-xl border border-border-default bg-bg-surface p-6">
          <div class="space-y-4">
            <div class="flex items-center gap-3 mb-4">
              <svg class="w-5 h-5 text-text-primary" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
              <span class="text-sm font-medium">Pull Request #142</span>
              <span class="inline-flex items-center px-2 py-0.5 rounded-full text-xs bg-fresh/10 text-fresh">open</span>
            </div>
            <div class="rounded-lg bg-bg-base p-4">
              <p class="text-sm font-medium mb-1">feat: implement OAuth flow</p>
              <p class="text-xs text-text-muted">andrewdeitrick opened 2 hours ago</p>
              <div class="mt-3 flex items-center gap-4 text-xs text-text-muted">
                <span class="flex items-center gap-1">
                  <span class="w-2 h-2 rounded-full bg-fresh"></span>
                  CI passing
                </span>
                <span>2 reviews</span>
                <span>+342 / -28</span>
              </div>
            </div>
            <div class="rounded-lg bg-bg-base p-4">
              <div class="flex items-center gap-2 mb-2">
                <div class="w-5 h-5 rounded-full bg-accent-purple/30"></div>
                <span class="text-xs font-medium">reviewer</span>
                <span class="text-xs text-text-muted">· 1h ago</span>
              </div>
              <p class="text-xs text-text-secondary">LGTM! One minor suggestion on the token refresh logic.</p>
            </div>
          </div>
        </div>
        <div class="order-1 lg:order-2">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-text-muted/10 text-text-secondary text-xs font-medium mb-4">
            <svg class="w-3.5 h-3.5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
            GitHub
          </div>
          <h3 class="text-2xl sm:text-3xl font-bold mb-4">GitHub in your workflow</h3>
          <p class="text-text-secondary leading-relaxed">Link PRs to tasks. Get notifications, CI status, and review requests right where you're working. No more tab-switching to github.com.</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add Features to index.astro**

Update `src/pages/index.astro` — add import and component after `<ProblemStatement />`:

```astro
---
import Layout from "../layouts/Layout.astro";
import Nav from "../components/Nav.astro";
import Hero from "../components/Hero.astro";
import ProblemStatement from "../components/ProblemStatement.astro";
import Features from "../components/Features.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <Nav />
  <main>
    <Hero />
    <ProblemStatement />
    <Features />
  </main>
</Layout>
```

- [ ] **Step 3: Verify all four feature blocks render with alternating layout**

Expected: Alternating text-left/text-right blocks. Terminal mockups with colored text. Staleness dots with green/orange/red. GitHub PR card with review.

- [ ] **Step 4: Commit**

```bash
git add src/components/Features.astro src/pages/index.astro
git commit -m "feat: add feature showcase section with four feature blocks"
```

---

### Task 7: Team Features Section

**Files:**
- Create: `src/components/TeamFeatures.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the TeamFeatures component**

Write `src/components/TeamFeatures.astro`:

```astro
<section class="py-24 px-6">
  <div class="max-w-4xl mx-auto">
    <div class="rounded-2xl border border-border-default bg-bg-surface p-10 sm:p-14 text-center relative overflow-hidden">
      <!-- Background glow -->
      <div class="absolute top-0 right-0 w-[300px] h-[300px] rounded-full bg-accent-purple/5 blur-[80px] pointer-events-none"></div>
      <div class="absolute bottom-0 left-0 w-[300px] h-[300px] rounded-full bg-accent-blue/5 blur-[80px] pointer-events-none"></div>

      <div class="relative">
        <h2 class="text-3xl sm:text-4xl font-bold mb-6">See what your team is working on</h2>
        <p class="text-text-secondary max-w-xl mx-auto leading-relaxed mb-10">Real-time presence shows who's active, idle, or offline — and which task they're on. Shared workspace, shared visibility. No standups needed to know what's in flight.</p>

        <!-- Presence mockup -->
        <div class="max-w-sm mx-auto space-y-3">
          <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base text-left">
            <div class="relative">
              <div class="w-8 h-8 rounded-full bg-gradient-to-br from-accent-purple to-accent-blue"></div>
              <div class="absolute -bottom-0.5 -right-0.5 w-3 h-3 rounded-full bg-fresh border-2 border-bg-surface"></div>
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-sm font-medium">Sarah</p>
              <p class="text-xs text-text-muted truncate">Working on: Auth flow refactor</p>
            </div>
            <span class="text-xs text-fresh">active</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base text-left">
            <div class="relative">
              <div class="w-8 h-8 rounded-full bg-gradient-to-br from-accent-green to-accent-blue"></div>
              <div class="absolute -bottom-0.5 -right-0.5 w-3 h-3 rounded-full bg-warm border-2 border-bg-surface"></div>
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-sm font-medium">Marcus</p>
              <p class="text-xs text-text-muted truncate">Working on: Fix CI pipeline</p>
            </div>
            <span class="text-xs text-warm">idle</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-lg bg-bg-base text-left">
            <div class="relative">
              <div class="w-8 h-8 rounded-full bg-gradient-to-br from-warm to-stale"></div>
              <div class="absolute -bottom-0.5 -right-0.5 w-3 h-3 rounded-full bg-text-muted border-2 border-bg-surface"></div>
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-sm font-medium text-text-muted">Jordan</p>
              <p class="text-xs text-text-muted truncate">Last seen: 3h ago</p>
            </div>
            <span class="text-xs text-text-muted">offline</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add TeamFeatures to index.astro**

Update `src/pages/index.astro` — add import `TeamFeatures` and place `<TeamFeatures />` after `<Features />`.

- [ ] **Step 3: Verify the centered team card renders with presence mockup**

Expected: Large card with heading, description, and three presence rows (active/idle/offline) with colored status dots and avatar placeholders.

- [ ] **Step 4: Commit**

```bash
git add src/components/TeamFeatures.astro src/pages/index.astro
git commit -m "feat: add team features section with presence mockup"
```

---

### Task 8: Pricing Section

**Files:**
- Create: `src/components/Pricing.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the Pricing component**

Write `src/components/Pricing.astro`:

```astro
<section id="pricing" class="py-24 px-6">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-3xl sm:text-4xl font-bold text-center mb-4">Simple pricing</h2>
    <p class="text-text-secondary text-center mb-16">Start free. Upgrade when you need more.</p>

    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
      <!-- Free -->
      <div class="rounded-xl border border-border-default bg-bg-surface p-8">
        <h3 class="text-lg font-semibold mb-2">Free</h3>
        <div class="mb-6">
          <span class="text-4xl font-bold">$0</span>
        </div>
        <ul class="space-y-3 mb-8">
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            1 project
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Unlimited tasks
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Unlimited terminals
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            GitHub integration
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Git worktree isolation
          </li>
        </ul>
        <a href="#download" class="block w-full text-center py-3 rounded-lg border border-border-default text-text-primary text-sm font-semibold hover:bg-bg-surface-raised transition">Download for free</a>
      </div>

      <!-- Pro -->
      <div class="rounded-xl border border-accent-green/40 bg-bg-surface p-8 relative">
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 px-3 py-1 rounded-full bg-accent-green text-bg-base text-xs font-semibold">Most popular</div>
        <h3 class="text-lg font-semibold mb-2">Pro</h3>
        <div class="mb-6">
          <span class="text-4xl font-bold">$10</span>
          <span class="text-text-muted text-sm">/month</span>
        </div>
        <ul class="space-y-3 mb-8">
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Everything in Free
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Unlimited projects
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Team workspaces
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Real-time collaboration
          </li>
          <li class="flex items-center gap-3 text-sm text-text-secondary">
            <svg class="w-4 h-4 text-accent-green flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
            Priority support
          </li>
        </ul>
        <a href="#download" class="block w-full text-center py-3 rounded-lg bg-accent-green text-bg-base text-sm font-semibold hover:brightness-110 transition shadow-lg shadow-accent-green/20">Start free trial</a>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add Pricing to index.astro**

Update `src/pages/index.astro` — add import `Pricing` and place `<Pricing />` after `<TeamFeatures />`.

- [ ] **Step 3: Verify two pricing cards render side by side**

Expected: Free card with outline CTA, Pro card with green border + badge + filled CTA. Cards stack on mobile.

- [ ] **Step 4: Commit**

```bash
git add src/components/Pricing.astro src/pages/index.astro
git commit -m "feat: add pricing section with Free and Pro cards"
```

---

### Task 9: Final CTA and Footer

**Files:**
- Create: `src/components/FinalCTA.astro`
- Create: `src/components/Footer.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Build the FinalCTA component**

Write `src/components/FinalCTA.astro`:

```astro
<section id="download" class="py-24 px-6 relative overflow-hidden">
  <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[400px] rounded-full bg-accent-purple/8 blur-[100px] pointer-events-none"></div>
  <div class="relative max-w-2xl mx-auto text-center">
    <h2 class="text-3xl sm:text-4xl lg:text-5xl font-bold mb-6">Stop juggling.<br />Start braiding.</h2>
    <a href="#" class="inline-flex items-center px-8 py-3.5 rounded-xl bg-accent-green text-bg-base font-semibold text-base hover:brightness-110 transition shadow-lg shadow-accent-green/20">
      Download for Mac
    </a>
    <p class="mt-6 text-text-muted text-sm">Available for macOS. Windows &amp; Linux coming soon.</p>
  </div>
</section>
```

- [ ] **Step 2: Build the Footer component**

Write `src/components/Footer.astro`:

```astro
<footer class="border-t border-border-default py-8 px-6">
  <div class="max-w-6xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
    <div class="flex items-center gap-3">
      <img src="/braid-logo.png" alt="Braid" class="w-6 h-6 rounded" />
      <span class="text-sm text-text-muted">&copy; 2026 Braid</span>
    </div>
    <div class="flex items-center gap-6">
      <a href="https://github.com/andrewdeitrick" class="text-sm text-text-muted hover:text-text-primary transition-colors">GitHub</a>
      <a href="https://x.com" class="text-sm text-text-muted hover:text-text-primary transition-colors">Twitter</a>
      <a href="mailto:hello@braid.software" class="text-sm text-text-muted hover:text-text-primary transition-colors">Contact</a>
    </div>
  </div>
</footer>
```

- [ ] **Step 3: Add FinalCTA and Footer to index.astro**

Update `src/pages/index.astro` to the final version with all components:

```astro
---
import Layout from "../layouts/Layout.astro";
import Nav from "../components/Nav.astro";
import Hero from "../components/Hero.astro";
import ProblemStatement from "../components/ProblemStatement.astro";
import Features from "../components/Features.astro";
import TeamFeatures from "../components/TeamFeatures.astro";
import Pricing from "../components/Pricing.astro";
import FinalCTA from "../components/FinalCTA.astro";
import Footer from "../components/Footer.astro";
---

<Layout title="Braid — Tame the chaos of parallel development" description="Braid weaves your AI-powered workflows into a single, organized interface. Tasks, terminals, and GitHub — all braided together.">
  <Nav />
  <main>
    <Hero />
    <ProblemStatement />
    <Features />
    <TeamFeatures />
    <Pricing />
    <FinalCTA />
  </main>
  <Footer />
</Layout>
```

- [ ] **Step 4: Verify full page renders end-to-end**

Run dev server and scroll through all sections. Expected: Smooth dark-themed page with all seven sections, responsive on mobile, all anchor links work.

- [ ] **Step 5: Commit**

```bash
git add src/components/FinalCTA.astro src/components/Footer.astro src/pages/index.astro
git commit -m "feat: add final CTA and footer, complete landing page"
```

---

### Task 10: Build and Verify Production Output

**Files:**
- No new files

- [ ] **Step 1: Run production build**

Run:
```bash
cd /Users/andrewdeitrick/workspace/braid.software
npx astro build
```

Expected: Build completes successfully, output in `dist/` directory.

- [ ] **Step 2: Preview production build**

Run:
```bash
cd /Users/andrewdeitrick/workspace/braid.software
npx astro preview
```

Expected: Production site serves at `localhost:4321`, all sections render, images load, no console errors.

- [ ] **Step 3: Commit any build config adjustments if needed**

If the build required changes, commit them. Otherwise skip.
