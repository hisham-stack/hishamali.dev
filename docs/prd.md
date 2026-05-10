# Portfolio Website — Product Requirements Document

|                                  |                                                                                     |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| **Owner**                        | Hisham Ali                                                                          |
| **Status**                       | v1.1 — open decisions resolved, ready for implementation                            |
| **Last updated**                 | 2026-05-09                                                                          |
| **Target audience for this doc** | Implementing developer (Hisham, or any senior full-stack engineer he hands this to) |
| **Estimated build effort**       | 2–3 focused weekends                                                                |

---

## 1. Overview

A personal portfolio website for Hisham Ali, a full-stack developer based in Lund, Sweden, targeting junior to mid-level developer roles in the Swedish tech market. The site is the primary online presence backing the candidate's CV, GitHub profile, and LinkedIn — a focused, professionally executed showcase of recent work, technical depth, and trajectory.

The site is intentionally small in surface area but built to a high quality bar. It functions both as **content** (work samples, narrative, contact) and as **evidence** (the codebase itself is a sample of the developer's work and is expected to be inspected by recruiters and engineering managers).

Visual direction is **minimal monochrome**: no accent colour, restrained motion, typography-led hierarchy, generous whitespace.

---

## 2. Goals & Non-Goals

### 2.1 Goals

- Establish a credible, professional online presence at a custom domain.
- Showcase three flagship projects (NordicMatch, SpeedMate, Resume LaTeX UI) with real technical depth.
- Communicate a distinctive narrative (multidisciplinary background, AI-augmented engineering, trilingual professional).
- Provide an accessible, performant, well-coded reference implementation that itself demonstrates engineering craft.
- Drive recruiters and hiring managers to a clear, low-friction contact path.

### 2.2 Non-Goals

- A blogging platform with a high publication cadence.
- A CMS or admin UI.
- E-commerce, authentication, user accounts, or social features.
- A design portfolio in the visual-design sense (no heavy imagery, animation showcases, or interactive art).
- A general-purpose marketing site.

---

## 3. Target Audience

| Persona                         | Need                                   | What they look for                                                               |
| ------------------------------- | -------------------------------------- | -------------------------------------------------------------------------------- |
| Swedish recruiter (technical)   | Quickly verify candidate substance     | Stack alignment, recent work, location, language, contactability                 |
| Engineering hiring manager      | Assess engineering judgement and craft | Real projects with depth, code quality of the site itself, written communication |
| Fellow engineer / peer reviewer | Evaluate technical credibility         | Architecture choices, repo hygiene, willingness to discuss trade-offs            |
| Future self                     | Maintainable artefact                  | Clean structure, low operational burden, easy to refresh                         |

Primary audience is the first two. All design and content decisions optimise for their first 30–90 second scan.

---

## 4. Success Metrics

**Quantitative**

- Lighthouse score ≥ 95 across Performance, Accessibility, Best Practices, SEO on both home and a representative case study page.
- Largest Contentful Paint < 1.5s on a simulated 4G connection.
- First-load JavaScript per route < 100 KB gzipped.
- Total transferred bytes on the home page < 500 KB.
- 100% AA WCAG 2.2 conformance on automated and manual checks.

**Qualitative**

- Site renders correctly on iOS Safari, Android Chrome, and the latest two versions of Chrome, Firefox, Safari and Edge on desktop.
- A recruiter can find email, LinkedIn, and GitHub within 5 seconds of landing.
- Each case study answers four questions: what was the problem, what did I build, what were the trade-offs, what was the outcome.

---

## 5. Scope — Version 1.0

**In scope**

- Single statically rendered website deployed to Vercel.
- One language: English.
- Five page types: Home, About, Work index, Work case study (parameterised), Contact.
- Three published case studies: NordicMatch, SpeedMate, Resume LaTeX UI.
- Privacy-friendly analytics.
- Custom domain, HTTPS, dynamic OG image, sitemap, `robots.txt`.
- Light theme only.

**Explicitly out of scope for v1.0** (deferred to roadmap, see §20)

- Swedish translation.
- Dark mode.
- Blog / writing section.
- Contact form with backend.
- RSS feed.
- Comments.
- Authentication.

---

## 6. Information Architecture

### 6.1 Sitemap

```
/
├── /about
├── /work
│   ├── /work/nordicmatch
│   ├── /work/speedmate
│   └── /work/resume-latex-ui
├── /contact
└── /404
```

### 6.2 Primary navigation

A single horizontal navigation, persistent on every page: **Home · About · Work · Contact**. Sticky on scroll on the home page only; static on inner pages. The wordmark on the left links home.

### 6.3 Footer

Minimal: copyright year, "Built with Next.js, hosted on Vercel" attribution, plus three small links (email, GitHub, LinkedIn). No newsletter, no social grid, no sitemap link.

---

## 7. Page Specifications

### 7.1 Home (`/`)

A compact, doorway-style page.

Sections, in order:

1. **Hero block** (above the fold) — **stacked layout**: large name on two lines ("Hisham" / "Ali"), then role line, then value proposition, then status badge, then action pair. Each element on its own row with vertical rhythm; no side-by-side splitting.
   - Name as primary heading: **Hisham Ali**.
   - Role line: "Full-Stack Developer · Lund, Sweden".
   - One-sentence value proposition (≤ 25 words).
   - Status badge: "Open to junior / mid-level roles".
   - Two primary actions: `View work →` (anchor to `/work`) and `Get in touch →` (anchor to `/contact`).
2. **Selected work** — three cards, one per featured case study. Each card: project name, one-line description, key tech tags rendered as plain inline text (not pill chips), link to the case study.
3. **Brief intro paragraph** (2–3 sentences) with a `Read more →` link to `/about`.
4. **Footer**.

No carousels, no autoplaying media, no marquee text.

### 7.2 About (`/about`)

Long-form prose page. First-person, conversational, professional. No marketing voice.

Structure:

- Page heading.
- Section 1 — _Where I am now_: current focus, stack, what I'm building.
- Section 2 — _How I got here_: the narrative arc — Damascus → systems analyst at SSRC → relocation → Komvux → Teknikhögskolan → developer. Framed as evidence of resilience and learning capacity, not as biography.
- Section 3 — _How I work_: AI-augmented development, formal CS fundamentals, systems thinking inherited from the SSRC role.
- Section 4 — _Outside work_: photography, languages, travel.
- End-of-page facts block: languages with CEFR levels, location & availability, current focus, selected coursework / distinctions.

Length target: 600–900 words.

### 7.3 Work index (`/work`)

A simple list view of all case studies. Each entry shows:

- Project name (heading).
- One-paragraph description (40–60 words).
- Stack as inline text.
- Year.
- "Read case study →" link.

Sorted reverse-chronological. No filtering or tagging in v1.

### 7.4 Work case study (`/work/[slug]`)

Authored as MDX (see §10.4 and Appendix A). Each case study follows a consistent template with the following sections:

- Title.
- One-line summary.
- Metadata strip: role, year, stack, links (live, repo).
- **Context** — what was the problem, who was it for.
- **Approach** — what I built and why, with architectural choices called out.
- **Trade-offs** — what I considered and rejected.
- **Outcome** — what shipped, what I learned, numbers where possible.
- Optional: architecture diagram (inline monochrome SVG).

No screenshot-only case studies. Every case study must be readable as standalone writing.

### 7.5 Contact (`/contact`)

Minimal page. No form in v1.

- Page heading.
- Short paragraph indicating availability and preferred channels.
- Email (`mailto:`), LinkedIn, GitHub as plain text links with the small external-link arrow.
- Location and timezone.

### 7.6 404

Plain page. Heading, one-line message ("That page doesn't exist."), link back to home. Same chrome as the rest of the site.

---

## 8. Visual Design System

### 8.1 Design principles

1. **Restraint over decoration.** Every element earns its place; when in doubt, remove it.
2. **Typography carries the design.** Hierarchy, rhythm and contrast come from type scale and weight, not from colour or ornament.
3. **Generous whitespace.** Vertical rhythm and breathing room are non-negotiable.
4. **Content-first.** Layout serves the writing; the writing is the product.
5. **Consistent monochrome.** No accent colours, no gradients, no shadows beyond the subtlest elevation cues.

### 8.2 Colour palette (light theme — the only theme in v1)

| Token                 | Hex       | Use                                  |
| --------------------- | --------- | ------------------------------------ |
| `--background`        | `#FAFAFA` | Page background                      |
| `--surface`           | `#FFFFFF` | Elevated surfaces (cards, callouts)  |
| `--foreground`        | `#0A0A0A` | Primary text                         |
| `--muted-foreground`  | `#52525B` | Secondary text, metadata             |
| `--subtle-foreground` | `#A1A1AA` | Tertiary text, captions              |
| `--border`            | `#E4E4E7` | Hairline dividers, card borders      |
| `--border-strong`     | `#D4D4D8` | Emphasised dividers, diagram strokes |
| `--focus-ring`        | `#0A0A0A` | Keyboard focus indicator             |
| `--selection-bg`      | `#0A0A0A` | Text selection background            |
| `--selection-fg`      | `#FAFAFA` | Text selection foreground            |

No accent colour. Links are styled with the foreground colour and an underline that appears or thickens on hover. The selection highlight is the only place where the page inverts, and that is deliberate.

All tokens declared as CSS custom properties in `styles/tokens.css` and consumed via Tailwind's `theme.extend.colors` mapping.

### 8.3 Typography

All typefaces self-hosted via `next/font/google` for zero layout shift and optimal performance.

| Role           | Family     | Weights       | Notes                       |
| -------------- | ---------- | ------------- | --------------------------- |
| Display & body | Geist Sans | 400, 500, 600 | Primary face for everything |
| Mono           | Geist Mono | 400, 500      | Dates, code, small metadata |

Geist Sans alone carries the entire design — display, body, UI, navigation. **No editorial serif accent.** This is a deliberate restraint choice consistent with the minimal-monochrome direction; one family for prose and UI, one mono face for metadata, nothing else.

**Type scale** (rem, base 16px):

| Token          | Size             | Line height | Weight | Use                           |
| -------------- | ---------------- | ----------- | ------ | ----------------------------- |
| `text-display` | 4.5rem (72px)    | 1.05        | 500    | Hero name (mobile: 3rem)      |
| `text-h1`      | 3rem (48px)      | 1.1         | 500    | Page titles (mobile: 2.25rem) |
| `text-h2`      | 2rem (32px)      | 1.2         | 500    | Section headings              |
| `text-h3`      | 1.5rem (24px)    | 1.3         | 500    | Subsection headings           |
| `text-h4`      | 1.25rem (20px)   | 1.4         | 500    | Card titles                   |
| `text-body`    | 1.0625rem (17px) | 1.65        | 400    | Body prose                    |
| `text-small`   | 0.9375rem (15px) | 1.55        | 400    | Secondary copy                |
| `text-meta`    | 0.8125rem (13px) | 1.5         | 500    | Metadata strips (mono)        |

Letter-spacing: `-0.02em` on display sizes, `-0.01em` on h1–h2, default elsewhere. Maximum line length for body prose: **68 characters** (use `max-w-[68ch]`).

### 8.4 Spacing and layout

Spacing scale, in pixels (multiples of 4): **4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128, 160**. Implemented through Tailwind's default scale.

Layout:

- Maximum content width: **720px** for prose pages (About, case studies), **960px** for the work index, **640px** for the contact page.
- Page horizontal padding: 24px on mobile, 48px on tablet, scales with viewport on desktop.
- Vertical rhythm: 96px between major page sections on desktop, 64px on mobile.

No formal grid system. Use CSS flexbox and grid pragmatically; centred single-column for prose.

### 8.5 Iconography

Icons from `lucide-react` only. Sized 16px or 20px, stroke width 1.5. Used very sparingly: external-link indicators, navigation hints, contact link prefixes. Never decoratively.

### 8.6 Imagery

The site contains no decorative photography in v1. Imagery is permitted only as:

- Architecture diagrams (inline SVG, monochrome, hairline strokes matching `--border-strong`).
- A single optional headshot on the About page (square crop, max 240px, desaturated to grayscale).
- The Open Graph social card (generated dynamically by `app/og/route.tsx`).

### 8.7 Motion

Restrained and purposeful.

- All transitions: 150ms, `cubic-bezier(0.4, 0, 0.2, 1)`.
- Hover states only on interactive elements (links, buttons).
- Page transitions: none — default browser behaviour.
- One subtle entrance animation acceptable: hero text fade-in over 300ms on initial load.
- Respect `prefers-reduced-motion: reduce` — disable all non-essential motion.

No parallax, no scroll-jacking, no autoplay video, no loading spinners (the site loads instantly).

---

## 9. Component Inventory

A small set of components is sufficient. Built on shadcn/ui where useful; most are bespoke and small.

| Component       | Notes                                                                 |
| --------------- | --------------------------------------------------------------------- |
| `SiteHeader`    | Wordmark + primary nav                                                |
| `SiteFooter`    | Persistent across pages                                               |
| `Hero`          | Home page hero block                                                  |
| `WorkCard`      | Used on home (selected work) and work index                           |
| `Prose`         | Wraps About and case study content with consistent typography         |
| `MetadataStrip` | Top of case study: role, year, stack, links inline                    |
| `ExternalLink`  | Adds `rel="noopener noreferrer"`, `target="_blank"`, small arrow icon |
| `MDXComponents` | Custom renderers for h2, h3, p, ul, code, pre, blockquote             |

shadcn/ui components to install: `button`, `separator`. That is the entire list. Anything more is over-engineering.

---

## 10. Technical Architecture

### 10.1 Stack

| Layer                | Choice                                    | Version                                              |
| -------------------- | ----------------------------------------- | ---------------------------------------------------- |
| Framework            | Next.js (App Router)                      | 15.x                                                 |
| UI library           | React                                     | 19.x                                                 |
| Language             | TypeScript                                | 5.x, `strict: true`                                  |
| Styling              | Tailwind CSS                              | 4.x (or 3.4 if 4 has blockers in target environment) |
| Component primitives | shadcn/ui                                 | latest                                               |
| Content authoring    | MDX                                       | via `@next/mdx` for Next 15                          |
| Frontmatter          | `gray-matter` + Zod schema                | latest                                               |
| Icons                | `lucide-react`                            | latest                                               |
| Fonts                | Geist Sans, Geist Mono                    | via `next/font/google`                               |
| Analytics            | Vercel Analytics                          | latest                                               |
| Linting              | ESLint flat config + `eslint-config-next` | latest                                               |
| Formatting           | Prettier + `prettier-plugin-tailwindcss`  | latest                                               |
| Tests                | Vitest (unit), Playwright (smoke)         | latest                                               |
| Package manager      | pnpm                                      | latest                                               |
| Node                 | 20 LTS minimum (22 LTS preferred)         | —                                                    |

### 10.2 Rendering strategy

All pages are statically rendered at build time (`export const dynamic = 'force-static'`). No runtime data fetching, no API routes in v1 except the OG image route which is statically cacheable. Revalidation is unnecessary — redeploy to update.

### 10.3 Repository structure

```
portfolio/
├── app/
│   ├── (site)/
│   │   ├── layout.tsx
│   │   ├── page.tsx                 # Home
│   │   ├── about/
│   │   │   └── page.tsx
│   │   ├── work/
│   │   │   ├── page.tsx             # Index
│   │   │   └── [slug]/
│   │   │       └── page.tsx         # Case study
│   │   ├── contact/
│   │   │   └── page.tsx
│   │   └── not-found.tsx
│   ├── og/
│   │   └── route.tsx                # Dynamic OG image
│   ├── globals.css
│   ├── robots.ts
│   ├── sitemap.ts
│   └── layout.tsx                   # Root layout (font, metadata, JSON-LD)
├── components/
│   ├── ui/                          # shadcn primitives
│   ├── site-header.tsx
│   ├── site-footer.tsx
│   ├── hero.tsx
│   ├── work-card.tsx
│   ├── prose.tsx
│   ├── metadata-strip.tsx
│   ├── external-link.tsx
│   └── mdx-components.tsx
├── content/
│   └── work/
│       ├── nordicmatch.en.mdx
│       ├── speedmate.en.mdx
│       └── resume-latex-ui.en.mdx
├── lib/
│   ├── content.ts                   # MDX loader + frontmatter Zod schema
│   ├── metadata.ts                  # Reusable Next Metadata helpers
│   ├── i18n.ts                      # Locale constants and helpers (forward-compatible)
│   └── seo.ts                       # JSON-LD generators
├── messages/
│   └── en.json                      # UI string catalogue (see §11)
├── public/
│   ├── favicon.ico
│   ├── icon.svg
│   ├── apple-icon.png
│   └── og-default.png               # Static fallback OG image
├── styles/
│   └── tokens.css                   # CSS custom properties
├── .github/
│   └── workflows/
│       └── ci.yml
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── eslint.config.mjs
├── prettier.config.mjs
├── package.json
├── pnpm-lock.yaml
└── README.md
```

### 10.4 Content authoring (MDX)

Case studies live in `content/work/{slug}.en.mdx`. The `.en` segment is mandatory in v1 to keep the loader forward-compatible with future locales (see §11).

Each file has YAML frontmatter:

```yaml
---
title: 'NordicMatch'
slug: 'nordicmatch'
summary: 'A full-stack matching platform built on Next.js 15 with split deployment across Vercel and Fly.io.'
year: 2026
role: 'Solo developer'
stack:
  [
    'Next.js 15',
    'TypeScript',
    'PostgreSQL',
    'Drizzle ORM',
    'BullMQ',
    'Redis',
    'Gotenberg',
  ]
links:
  live: 'https://example.com' # optional
  repo: 'https://github.com/...' # optional
status: 'published' # or "draft"
order: 1
---
```

Frontmatter is parsed with `gray-matter` and validated against a Zod schema in `lib/content.ts`. The loader enumerates the directory, filters `status: "published"`, sorts by `order` then `year`, and exposes typed accessors used by the work index and case study pages.

`generateStaticParams()` returns the slugs at build time so every published case study is pre-rendered.

### 10.5 SEO and metadata

- `generateMetadata()` per page (title, description, canonical URL, OG image, Twitter card).
- Title format: `{Page} — Hisham Ali` (the home page is just `Hisham Ali — Full-Stack Developer`).
- Default OG image rendered via `next/og` from `app/og/route.tsx`: name + role on the brand background, statically cached.
- Per-case-study OG images use the same template with the case study title.
- JSON-LD: `Person` schema in the root layout; `CreativeWork` per case study.
- `app/sitemap.ts` enumerates static routes plus published case studies.
- `app/robots.ts` allows everything except `/api/*` — the rule is forward-compatible even though no API routes exist in v1.

### 10.6 Analytics

**Vercel Analytics.** Zero-config, free on the Hobby tier, GDPR-compliant without a cookie consent prompt, no extra account to manage. Install `@vercel/analytics` and mount the `<Analytics />` component in the root layout. No custom event tracking in v1.

### 10.7 Forms

No forms in v1. Contact is via `mailto:` links. If a contact form is added later (§20), use a Next.js Server Action plus Resend or Postmark; do not introduce a client-side form library before it is needed.

---

## 11. Internationalization Strategy

### 11.1 v1 (English-only)

The site ships in English only. The codebase is structured so that adding Swedish later is a localised, low-risk change rather than a refactor.

**Day-1 commitments to enable this:**

1. **All user-facing UI copy lives in a translation catalogue at `messages/en.json`**, not hardcoded in JSX. Even though only English exists, every visible string is referenced via a `t('home.hero.title')`-style key. A small typed helper in `lib/i18n.ts` exposes `t(key)` reading from the JSON file at build time. This keeps the pattern in place without taking the runtime cost of a full i18n library.
2. **No locale-coupled formatting in components.** Dates, numbers and lists are formatted via `Intl.DateTimeFormat`, `Intl.NumberFormat` and `Intl.ListFormat` with the active locale (`'en'`) passed in explicitly — never with the runtime default.
3. **MDX content uses a locale-aware filename convention from day one**: `content/work/{slug}.{locale}.mdx`. v1 ships `content/work/{slug}.en.mdx`; the loader resolves `.en.mdx` by default.
4. **Routing is left flat (`/about`, `/work`)** in v1 to avoid an unnecessary `/en/...` prefix while only one locale exists. The middleware-driven prefixing is added in v1.1.
5. **`<html lang>` is set from a constant**, ready to switch from `'en'` to a dynamic value.

These five commitments are the entire i18n investment in v1. They do not require installing `next-intl` or any other library yet.

### 11.2 v1.1 (adding Swedish)

When Swedish is added:

- Adopt **`next-intl`** (App Router native, type-safe, server-component friendly). Install, wire up `i18n.ts` and `middleware.ts`.
- Move pages into `app/[locale]/...`. Add `locale` to all generated metadata and OG images.
- Translation catalogues: `messages/en.json` and `messages/sv.json`. Every key in `en.json` must exist in `sv.json` — enforce in CI.
- Default locale: `en`. Locale negotiation order: URL prefix → first-party cookie → `Accept-Language` header → fallback to default. Persist user choice in a first-party cookie.
- Locale switcher in the site header. The active locale is the one in the URL.
- MDX case studies: each case study has paired `.en.mdx` and `.sv.mdx` files. If a Swedish file is missing, fall back to English with a small inline notice.
- `sitemap.ts` enumerates both locales and emits `hreflang` alternates.
- Translation done by Hisham personally; no machine translation in production copy.

This work is scoped to roughly one weekend of effort given the day-1 preparation above.

---

## 12. Performance Requirements

| Metric                      | Target           | Measurement                           |
| --------------------------- | ---------------- | ------------------------------------- |
| Lighthouse Performance      | ≥ 95             | PageSpeed Insights (mobile + desktop) |
| Lighthouse Accessibility    | ≥ 95             | PageSpeed Insights                    |
| Lighthouse Best Practices   | ≥ 95             | PageSpeed Insights                    |
| Lighthouse SEO              | 100              | PageSpeed Insights                    |
| LCP                         | < 1.5s (4G)      | Vercel Speed Insights or WebPageTest  |
| INP                         | < 200ms          | Real-user data via Plausible / Vercel |
| CLS                         | < 0.05           | Lighthouse                            |
| Page weight, home (gzipped) | < 500 KB         | Bundle analyser                       |
| First-load JS, any route    | < 100 KB gzipped | `next build` output                   |

**Practical constraints to hit these:**

- All routes statically rendered.
- All fonts self-hosted via `next/font` with `display: 'swap'`.
- All images via `next/image` with explicit width/height; `priority` only on the LCP element.
- Default to React Server Components; promote to client components only when interactivity demands it.
- No global state libraries.
- No client-side analytics SDK beyond a single small script.

---

## 13. Accessibility Requirements

- WCAG 2.2 AA conformance. Verified by `axe-core` (Playwright integration) and manual screen reader testing (VoiceOver on macOS, NVDA on Windows).
- Semantic HTML: one `<h1>` per page, headings in document order, `<nav>`, `<main>`, `<footer>` landmarks.
- Skip-to-content link, visible on keyboard focus.
- Visible focus indicators: 2px solid `--focus-ring`, 2px offset.
- Colour contrast ≥ 4.5:1 for body text, ≥ 3:1 for large text and UI components.
- `lang` attribute on `<html>` (constant `"en"` in v1, dynamic in v1.1).
- All interactive elements reachable and operable by keyboard.
- `prefers-reduced-motion: reduce` respected: disables hero entrance animation and all transitions beyond instant state changes.
- All meaningful images have `alt` text; decorative SVG diagrams use `role="img"` and `aria-label`.
- No forms in v1; mailto links and external links are clearly labelled.

---

## 14. Browser & Device Support

**Tier 1** (full support, tested every release): Latest two major versions of Chrome, Firefox, Safari, Edge desktop. iOS Safari 17+. Current Android Chrome.

**Tier 2** (best-effort, no visual regression bug fixes unless trivial): Older Safari/Chrome within the last 24 months.

**Tier 3** (unsupported, may degrade): Internet Explorer (any), legacy Edge.

Viewport range: **320px to 2560px**. Tested at 320, 375, 768, 1024, 1440, 2560.

---

## 15. Security & Privacy

- HTTPS enforced (Vercel default).
- Strict security headers via `next.config.ts` `headers()`:
  - `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`
  - `X-Content-Type-Options: nosniff`
  - `X-Frame-Options: DENY`
  - `Referrer-Policy: strict-origin-when-cross-origin`
  - `Permissions-Policy: camera=(), microphone=(), geolocation=()`
  - `Content-Security-Policy: default-src 'self'; script-src 'self' va.vercel-scripts.com; style-src 'self' 'unsafe-inline'; img-src 'self' data:; font-src 'self'; connect-src 'self' vitals.vercel-insights.com; frame-ancestors 'none'`.
- No cookies set in v1 (analytics is cookieless).
- No personal data collected via the site beyond what visitors voluntarily send via email.
- A short privacy note linked from the footer is sufficient; no consent banner required.
- Target an **A or A+ rating on `securityheaders.com`**.

---

## 16. Development Workflow

### 16.1 Tooling

- pnpm for package management.
- Node 20 LTS minimum, pinned via `.nvmrc` and `engines` in `package.json`.
- VS Code as the assumed editor; `.vscode/settings.json` includes format-on-save.

### 16.2 Scripts (`package.json`)

| Script         | Command                    |
| -------------- | -------------------------- |
| `dev`          | `next dev`                 |
| `build`        | `next build`               |
| `start`        | `next start`               |
| `lint`         | `eslint . && tsc --noEmit` |
| `format`       | `prettier --write .`       |
| `format:check` | `prettier --check .`       |
| `test`         | `vitest run`               |
| `test:e2e`     | `playwright test`          |
| `analyze`      | `ANALYZE=true next build`  |

### 16.3 Code quality gates

- ESLint: `eslint-config-next` plus `@typescript-eslint` recommended rules.
- Prettier with `prettier-plugin-tailwindcss` for class-name sorting.
- TypeScript: `strict`, `noUncheckedIndexedAccess`, `noImplicitOverride`.
- **Conventional commits, loosely.** Not strict tooling — discipline. Use `feat:`, `fix:`, `docs:`, `chore:`, `refactor:` prefixes. This helps the history read cleanly to a reviewer skimming `git log`.
- Pre-commit: `lint-staged` runs Prettier and ESLint on staged files.

### 16.4 Continuous integration

`.github/workflows/ci.yml` runs on every push and PR:

- pnpm install (cached).
- `pnpm lint`.
- `pnpm format:check`.
- `pnpm build`.
- `pnpm test`.
- Optional: Lighthouse CI against the Vercel preview URL.

### 16.5 Branching

`main` is always deployable and auto-deploys to production on Vercel. Feature work happens on branches → PR → preview deploy → review → squash merge.

### 16.6 Initial commit sequence

Get the scaffolding right _before_ the first feature commit. The single biggest mistake in portfolio repos is "I'll add ESLint/Prettier/CI later" — later never comes, and the early commits look amateur. Bake all of it in before any feature code ships.

The first three commits should be infrastructure only:

1. **`chore: initial Next.js scaffold`** — `create-next-app` output with TypeScript strict, ESLint flat config, Prettier with the Tailwind plugin, `.editorconfig`, `.nvmrc`, pnpm lockfile, comprehensive `.gitignore`, and a basic README. Nothing else.
2. **`chore: add design tokens`** — the CSS custom properties from §8.2 in `styles/tokens.css`, mapped through Tailwind's `theme.extend`.
3. **`chore: add CI`** — the GitHub Actions workflow from §16.4 (lint, format check, typecheck, build).

Only then start writing components, page by page. Each commit small, each one buildable.

---

## 17. Deployment & Hosting

| Item              | Choice                                                    |
| ----------------- | --------------------------------------------------------- |
| Host              | Vercel (Hobby tier is sufficient)                         |
| Domain            | `hishamali.dev` (registered)                              |
| DNS               | Registrar-managed CNAME / ALIAS to `cname.vercel-dns.com` |
| TLS               | Vercel-managed (Let's Encrypt)                            |
| Environments      | Production (`main`), Preview (per-PR), Local (`pnpm dev`) |
| Required env vars | None in v1 (Vercel Analytics is zero-config)              |
| Region            | Default (Vercel global edge)                              |

**Connect Vercel to the repo as soon as the first commit lands on `main`.** Preview deploys for every PR from day one are invaluable for sanity-checking visual changes against real rendering. Point the custom domain at Vercel after a handful of commits — even a scaffold-only page is fine to be live; nobody is looking yet, and getting DNS/HTTPS settled early avoids a launch-day scramble.

---

## 18. Content Requirements

The following original copy must be written before launch. Total: roughly 1,500 words.

| Surface                    | Word count              | Source                              |
| -------------------------- | ----------------------- | ----------------------------------- |
| Hero value proposition     | 1 sentence (≤ 25 words) | Original                            |
| Home intro paragraph       | 60–80 words             | Adapted from CV summary             |
| About page                 | 600–900 words           | Original, drafted from CV narrative |
| NordicMatch case study     | 600–800 words           | Original                            |
| SpeedMate case study       | 500–700 words           | Original (Combain LIA 2 work)       |
| Resume LaTeX UI case study | 400–600 words           | Original                            |
| Contact page intro         | 30–50 words             | Original                            |
| Footer attribution         | 1 line                  | Original                            |
| OG image text              | Name + role             | Static                              |

Each case study must include either an inline architecture diagram or an annotated code excerpt — never just prose.

---

## 19. Acceptance Criteria

The site is ready to launch when all of the following are true:

- [ ] All five page types implemented and rendering correctly.
- [ ] Three case studies authored, reviewed, and published.
- [ ] Lighthouse ≥ 95 across all four categories on Home and at least one case study.
- [ ] Manual screen reader pass on Home, About, and one case study.
- [ ] Tested on iOS Safari, Android Chrome, latest desktop Chrome and Safari.
- [ ] All security headers verified via `securityheaders.com` (target A or A+).
- [ ] Sitemap and `robots.txt` valid and submitted to Google Search Console.
- [ ] OG image renders correctly in LinkedIn, Slack, X, iMessage previews.
- [ ] No console errors or warnings in any tested browser.
- [ ] CI green: lint, format check, build, unit tests, smoke tests.
- [ ] Custom domain configured and HTTPS verified.
- [ ] Analytics receiving events from production.
- [ ] README documents setup, scripts, content authoring, and deployment.

---

## 20. Roadmap

### v1.0 — Launch

Everything described above.

### v1.1 — Swedish localisation

Adopt `next-intl`, introduce `[locale]` segment, translate UI strings and three case studies, locale switcher, `hreflang` alternates, per-locale OG images.

### v1.2 — Dark mode

Add `next-themes` and a theme toggle. Mirror all colour tokens for a dark theme. Persist preference, respect `prefers-color-scheme`.

### v1.3 — Writing

Add a `/notes` index for short essays (AI-augmented engineering, Next.js patterns, systems thinking). Same MDX authoring pattern as case studies. RSS feed at `/rss.xml`.

### v1.4 — Contact form

Server Action + Resend, honeypot, rate-limit, optional Cloudflare Turnstile if abuse appears.

### Speculative (no commitment)

Live "now" page, an interactive case study (e.g., embedded NordicMatch demo), a small `/uses` page.

---

## 21. Open Questions

| #   | Question                                                       | Status                                         |
| --- | -------------------------------------------------------------- | ---------------------------------------------- |
| 1   | ~~Final domain choice~~                                        | ✅ Resolved — `hishamali.dev` registered       |
| 2   | ~~Analytics provider~~                                         | ✅ Resolved — Vercel Analytics                 |
| 3   | Headshot on About page — yes or no                             | Open — decide before About page implementation |
| 4   | ~~Editorial serif accent~~                                     | ✅ Resolved — omitted; Geist Sans only         |
| 5   | NordicMatch case study — how much can be disclosed pre-launch? | Open — decide before case study draft          |

---

## Appendix A — Case study MDX template

```mdx
---
title: 'Project Name'
slug: 'project-name'
summary: 'One-line summary, 15–25 words.'
year: 2026
role: 'Solo developer'
stack: ['Next.js 15', 'TypeScript', '...']
links:
  live: 'https://...' # optional
  repo: 'https://github.com/...' # optional
status: 'published'
order: 1
---

## Context

What problem was this solving? Who was it for? What constraints shaped it?

## Approach

What I built and why. Call out one or two architectural decisions explicitly:
why this stack, why this boundary, why this trade-off.

## Trade-offs

What I considered and rejected. What I would do differently next time.

## Outcome

What shipped. What I learned. Numbers where possible.

<!-- Optional inline architecture diagram (SVG) -->
```

---

## Appendix B — References & inspiration

- **brittanychiang.com** — canonical developer portfolio reference
- **leerob.com** — idiomatic Next.js / Vercel execution
- **linear.app** — restraint, monochrome execution, type discipline
- **vercel.com** — typography and motion sensibility
- **pangrampangram.com** — typographic confidence

---

**End of document.**
