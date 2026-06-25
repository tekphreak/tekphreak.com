# CLAUDE.md — tekphreak.com Homepage Redesign

## Project Overview

Redesign the personal homepage at **tekphreak.com** (GitHub Pages, plain HTML/CSS/JS — no frameworks, no build tools).  
Goal: A warm, professional, recruiter- and headhunter-friendly landing page that positions the owner as a multi-disciplinary professional open to roles across IT/Technical Support, Security, and Software/App Development.

---

## Design Specification

### Palette (Warm & Professional)
| Token | Hex | Role |
|---|---|---|
| `--color-ink` | `#1C1C1E` | Body text, nav |
| `--color-surface` | `#FAF7F2` | Page background (warm off-white) |
| `--color-card` | `#FFFFFF` | Section/card backgrounds |
| `--color-accent` | `#8B5E3C` | CTA buttons, active states, highlight (warm cognac) |
| `--color-accent-light` | `#F0E6DA` | Subtle highlight bands, tag backgrounds |
| `--color-muted` | `#6B6B6B` | Captions, secondary labels |
| `--color-border` | `#E2D9CE` | Dividers, card borders |

### Typography
- **Display / Hero:** `'Playfair Display', Georgia, serif` — used only for the hero name and section headings. Signals gravitas.
- **Body:** `'Inter', system-ui, sans-serif` — clean and highly legible at all sizes.
- **Utility / Labels:** `'Inter'` at small caps or uppercase tracking — role tags, section eyebrows.
- Load both from Google Fonts:
  ```html
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  ```

### Type Scale
```
Hero name:        clamp(2.6rem, 6vw, 4.2rem), Playfair Display 700
Section heading:  clamp(1.6rem, 3vw, 2.2rem), Playfair Display 600
Subheading:       1.1rem, Inter 600
Body:             1rem / 1.75, Inter 400
Caption/label:    0.8rem, Inter 500 uppercase tracking
```

### Signature Element
A **thin cognac-colored left-border rule** on the hero tagline block — like a professional dossier annotation. This same motif repeats subtly on blockquotes, the "Open to Work" badge, and timeline entries. It's restrained, not decorative — it encodes "this detail was marked for attention."

---

## Page Structure

**This is a single scrolling page — no subpages.** All content lives in one file: `index.html`.  
CSS lives in `style.css`. No JavaScript framework. Minimal JS only if needed for mobile nav toggle.

### Sections (in order)

1. **`<nav>`** — Sticky top nav. Logo: "Michael" in Playfair Display. Right-side links: About, Skills, Experience, Projects, Certifications, Contact. On mobile: hamburger toggle.

2. **`#hero`** — Full-viewport-height intro.
   - Left column: Name (Playfair Display, large), one-line professional tagline, "Open to Opportunities" badge, two CTA buttons: **Download Resume** (primary, accent) + **Contact Me** (secondary, outlined).
   - Right column: Profile photo placeholder — a clean rounded rectangle with a subtle warm border and alt text "Photo coming soon." The `<img>` tag uses `src="assets/profile.jpg"` so the user can drop in a photo with no code changes.
   - Hero background: `--color-surface` with a very subtle warm grain texture via CSS (`background-image: url("data:image/svg+xml...")` or a noise overlay).

3. **`#about`** — 2-column layout. Left: short professional bio (3–4 sentences). Right: quick-stat cards (Years of Experience, Industries, Roles). Keep all copy placeholder-safe — use `[PLACEHOLDER]` tags for any personal details.

4. **`#skills`** — Tag-cloud style grouped by category: **Technical Support & IT**, **Security Operations**, **Software & App Development**, **Communication & Customer Service**, **Military / Signal Corps**. Tags styled with `--color-accent-light` background and `--color-accent` text.

5. **`#experience`** — Vertical timeline. Each entry: role title, company name, date range, 2–3 bullet responsibilities. Use the cognac left-border rule as the timeline spine. Entries: **[PLACEHOLDER — add your roles here]**.

6. **`#projects`** — 3-column card grid. Each card: project name, short description, tech tags, optional GitHub link button. Cards use `--color-card` with `--color-border` border and a subtle box-shadow on hover.

7. **`#certifications`** — Simple icon + label grid. Each cert: icon (Font Awesome or emoji fallback), cert name, issuing body, year. Placeholder entries included.

8. **`#contact`** — Centered section. Heading: "Let's Connect." Short line inviting recruiters and hiring managers to reach out. Links: Email (mailto), LinkedIn, GitHub. **Do not hardcode any email addresses or phone numbers in the HTML** — use `[YOUR_EMAIL]` placeholder. User will fill in manually.

9. **`<footer>`** — One line: name + year + "Built with care." No tracking, no third-party scripts.

---

## Resume Download

- Button in hero: `<a href="assets/resume.pdf" download class="btn btn-primary">Download Resume</a>`
- User drops their PDF into `assets/resume.pdf` — no code changes needed.
- If file is missing, the button should still render cleanly (no JS error).

---

## Privacy & Safety Rules (ENFORCE THESE)

- **Never** hardcode a real email address, phone number, home address, or personal URL into the HTML.
- Use `[YOUR_EMAIL]`, `[YOUR_LINKEDIN_URL]`, `[YOUR_GITHUB_URL]` as explicit placeholders.
- The profile photo path is `assets/profile.jpg` — do not fetch or embed any real photo.
- Resume path is `assets/resume.pdf` — do not embed resume content in the page.
- Add an HTML comment above each placeholder: `<!-- FILL IN BEFORE PUBLISHING -->`.

---

## Handling Existing Files

The repo already contains files. Follow these steps **before writing any new code:**

1. **Read all existing files first.** Run `ls -la` in the repo root and `cat` each file to understand what's there.
2. **Back up `index.html`** by copying it to `index.html.bak` before making any changes.
3. **Do not delete or overwrite** any file other than `index.html` unless explicitly instructed.
4. **Preserve any existing `assets/` folder contents** (images, PDFs, etc.) — do not remove them.
5. After creating the backup, do a **complete rewrite** of `index.html` per this spec.
6. If a `style.css` already exists, back it up to `style.css.bak` then replace it fully.
7. If a `script.js` already exists, back it up to `script.js.bak` then replace it with the minimal nav-toggle version.

> After each build iteration, the user will review locally in a browser before anything is pushed to GitHub. Do not run `git push` or any git commands unless explicitly asked.

---

## Iteration Workflow

This project uses a local review loop:

1. Claude Code builds or edits files locally.
2. User opens `index.html` in a browser to review.
3. User gives feedback for the next iteration.
4. Repeat until approved.
5. User pushes to GitHub Pages manually.

**Never commit or push to git without explicit user instruction.**

---

## File Structure

```
tekphreak.com/
├── index.html
├── style.css              (screen styles + responsive)
├── print.css              (print/PDF stylesheet)
├── script.js              (mobile nav toggle only — keep minimal)
├── robots.txt
├── sitemap.xml
├── site.webmanifest       (PWA/home screen icon support)
├── favicon.ico            ← drop your favicon here (repo root)
└── assets/
    ├── favicon-16x16.png  ← drop favicon files here
    ├── favicon-32x32.png
    ├── apple-touch-icon.png  (180x180)
    ├── favicon.svg           (optional, modern browsers)
    ├── profile.jpg        ← drop your photo here
    └── resume.pdf         ← drop your resume PDF here
```

> **Extensibility:** This structure is designed to grow. Future subpages (blog, portfolio, projects) are added as new HTML files alongside `index.html`. Shared styles stay in `style.css`; page-specific styles go in separate files (e.g. `blog.css`). Nav anchor links (`href="#section"`) become relative paths (`href="projects.html"`) when subpages are added.

---

## Responsiveness & Mobile

### Philosophy
Mobile visitors — especially recruiters — should land on what feels like a **scannable mini-resume**: name, title, open-to-work signal, and one-tap actions (call/email/resume) all visible before any scrolling. Every section below the fold should be readable with one thumb, no pinching.

### Viewport meta tag (required)
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Breakpoints (mobile-first)
| Breakpoint | Target | Key changes |
|---|---|---|
| default (< 480px) | Small phones | Single column everything, large tap targets |
| 480px | Large phones / small Android | Slight spacing increase |
| 768px | Tablets / landscape phone | 2-col layouts unlock, nav expands |
| 1024px | Desktop | Full 3-col grids, hero 2-col |

### Section-by-section mobile rules

**Nav**
- Collapses to hamburger at 768px
- Hamburger tap target minimum 44×44px (Apple HIG standard)
- Open menu is a full-width dropdown, not an overlay — easier to tap
- Active section highlighted via scroll spy (JS)
- `position: sticky; top: 0` on all screen sizes

**Hero (most important section)**
- Single column on mobile: name → tagline → badge → buttons stacked vertically
- Profile photo hidden on mobile (< 480px) to prioritize text content
- "Download Resume" and "Contact Me" buttons are full-width on mobile, minimum 48px tall
- Name font clamps down: `clamp(2rem, 8vw, 4.2rem)`
- "Open to Opportunities" badge always visible — do not hide on mobile

**About**
- 2-col → single col; stat cards stack vertically
- Stat cards become full-width with larger numbers for scannability

**Skills**
- Tag cloud wraps naturally — no changes needed
- Ensure tag font size never drops below 13px on mobile

**Experience (timeline)**
- Vertical timeline collapses: left-border rule becomes a top border rule on mobile
- Each entry is a full-width card with clear role title at top in bold
- Date range displayed as a small label above the role title
- Bullet points stay — they're the resume detail recruiters want

**Projects**
- 3-col → 2-col (768px) → 1-col (480px)
- On mobile, each card shows: title, 2-line description, tech tags, link button
- No hover effects on mobile (`:hover` only applies on pointer devices via `@media (hover: hover)`)

**Certifications**
- Grid: 3-col → 2-col → 1-col
- Each cert is a full-width row on small phones

**Contact**
- Email and LinkedIn links must be large tap targets (full-width buttons on mobile)
- Phone-friendly: `href="mailto:..."` and `href="tel:..."` formatted correctly

### Cross-platform specifics

**iOS Safari**
- Add `-webkit-overflow-scrolling: touch` to any scrollable containers
- Avoid `position: fixed` on anything except the nav — causes layout bugs in older Safari
- Use `env(safe-area-inset-*)` padding for notched iPhones:
  ```css
  padding-left: max(1rem, env(safe-area-inset-left));
  padding-right: max(1rem, env(safe-area-inset-right));
  ```
- Test tap targets: iOS requires 44px minimum

**Android Chrome**
- `theme-color` meta already set to cognac `#8B5E3C` — Chrome will tint the address bar
- Ensure font sizes never below 16px on inputs to prevent auto-zoom
- Test with Chrome DevTools device emulation at Galaxy A series resolution (360×800)

**General**
- No horizontal scrolling at any viewport width — `overflow-x: hidden` on `body`
- Images use `max-width: 100%` and `height: auto`
- All tap targets minimum 44×44px with adequate spacing between them
- Font sizes: body never below 16px on mobile to prevent Safari auto-zoom
- Use `em` or `rem` units — never `px` for font sizes in media queries
- Smooth scroll: `scroll-behavior: smooth` on `html` element
- Test at 320px width (iPhone SE) — the hardest constraint

---

## Accessibility

- All images have descriptive `alt` text.
- Color contrast meets WCAG AA (verified: cognac `#8B5E3C` on `#FAF7F2` passes).
- Keyboard-navigable nav with visible `:focus-visible` outlines.
- `prefers-reduced-motion` respected — no transforms or transitions when active.

---

## SEO & Discoverability

### Meta Tags (add to `<head>` of index.html)

```html
<!-- FILL IN BEFORE PUBLISHING -->
<meta name="description" content="[FULL_NAME] — [BRAND_NAME] | Technical Support, Security Operations & Software Development professional based in Atlanta, GA. Open to new opportunities.">
<meta name="keywords" content="[FULL_NAME], [BRAND_NAME], technical support specialist, security officer, software developer, Atlanta, IT professional, hire, resume">
<meta name="author" content="[FULL_NAME]">
<meta name="robots" content="index, follow">

<!-- Open Graph (LinkedIn, Facebook, recruiter tool previews) -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://tekphreak.com/">
<meta property="og:title" content="[FULL_NAME] | [BRAND_NAME] — Professional Portfolio">
<meta property="og:description" content="Technical Support, Security Operations & Software Development professional based in Atlanta, GA. Open to new opportunities.">
<meta property="og:image" content="https://tekphreak.com/assets/profile.jpg">

<!-- Twitter/X Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="[FULL_NAME] | [BRAND_NAME]">
<meta name="twitter:description" content="Technical Support, Security & Software Development professional. Open to new opportunities.">
<meta name="twitter:image" content="https://tekphreak.com/assets/profile.jpg">

<!-- Canonical URL -->
<link rel="canonical" href="https://tekphreak.com/">
```

### Structured Data — JSON-LD (add before `</body>`)

Person schema so Google shows a rich result when someone searches the owner's name:

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "[FULL_NAME]",
  "alternateName": "[BRAND_NAME]",
  "url": "https://tekphreak.com",
  "image": "https://tekphreak.com/assets/profile.jpg",
  "jobTitle": "[CURRENT_OR_TARGET_ROLE]",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Atlanta",
    "addressRegion": "GA",
    "addressCountry": "US"
  },
  "sameAs": [
    "[YOUR_LINKEDIN_URL]",
    "[YOUR_GITHUB_URL]"
  ]
}
```

> All `[PLACEHOLDER]` values must have an HTML comment `<!-- FILL IN BEFORE PUBLISHING -->` directly above them. Never hardcode real personal data.

### Page Title Tag

```html
<title>[FULL_NAME] | [BRAND_NAME] — Technical Support, Security & Software Development | Atlanta, GA</title>
```

### Heading Hierarchy (SEO-critical)

- One `<h1>` only — the hero name. Do not use `<h1>` anywhere else on the page.
- Section headings use `<h2>`.
- Sub-items within sections use `<h3>`.
- Never skip heading levels.

### sitemap.xml

Create `sitemap.xml` in the repo root:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://tekphreak.com/</loc>
    <lastmod>[YYYY-MM-DD]</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

---

## robots.txt

Create `robots.txt` in the repo root with this exact content:

```
# Allow all legitimate search crawlers
User-agent: *
Allow: /

# Block AI training bots
User-agent: GPTBot
Disallow: /

User-agent: ChatGPT-User
Disallow: /

User-agent: Claude-Web
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: anthropic-ai
Disallow: /

User-agent: CCBot
Disallow: /

User-agent: Google-Extended
Disallow: /

User-agent: Omgilibot
Disallow: /

User-agent: FacebookBot
Disallow: /

User-agent: Bytespider
Disallow: /

User-agent: Amazonbot
Disallow: /

# Sitemap location
Sitemap: https://tekphreak.com/sitemap.xml
```

---

## Recruiter/Headhunter UX Priorities

- Hero must communicate **name + what you do + open to work** in under 3 seconds.
- Resume download must be reachable without scrolling on desktop.
- Contact section should be the last thing a recruiter sees — make it easy to act.
- Avoid jargon in visible headings — use plain role titles recruiters search for.
- Add `<meta>` tags for SEO: `description`, `og:title`, `og:description`, `og:image`.

---

## What NOT to Do

- No dark mode (warm/professional palette is intentional).
- No parallax scrolling or heavy animations.
- No third-party analytics, tracking pixels, or ad scripts.
- No Lorem Ipsum — use honest placeholder labels like `[Role Title]` or `[Company Name]`.
- No inline styles — all styling via `style.css` CSS custom properties.
- Do not install npm, Node, or any build tool. This is pure HTML/CSS/JS.

---

## Favicon Support

The user will supply their own favicon files. Claude Code's job is to wire up all the correct `<link>` tags in `<head>` — nothing more. Do not generate, fetch, or create favicon image files.

### Required `<head>` tags

```html
<!-- Favicon — FILL IN BEFORE PUBLISHING (drop files into assets/ and favicon.ico into root) -->
<link rel="icon" type="image/x-icon" href="/favicon.ico">
<link rel="icon" type="image/png" sizes="32x32" href="/assets/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/assets/favicon-16x16.png">
<link rel="apple-touch-icon" sizes="180x180" href="/assets/apple-touch-icon.png">
<link rel="icon" type="image/svg+xml" href="/assets/favicon.svg">
<link rel="manifest" href="/site.webmanifest">
<meta name="theme-color" content="#8B5E3C">
```

### site.webmanifest

Create `site.webmanifest` in the repo root:

```json
{
  "name": "[FULL_NAME] | [BRAND_NAME]",
  "short_name": "[BRAND_NAME]",
  "icons": [
    { "src": "/assets/favicon-16x16.png", "sizes": "16x16", "type": "image/png" },
    { "src": "/assets/favicon-32x32.png", "sizes": "32x32", "type": "image/png" },
    { "src": "/assets/apple-touch-icon.png", "sizes": "180x180", "type": "image/png" }
  ],
  "theme_color": "#8B5E3C",
  "background_color": "#FAF7F2",
  "display": "browser"
}
```

### Favicon file checklist (user supplies these)

| File | Size | Where |
|---|---|---|
| `favicon.ico` | 16×16 + 32×32 multi-size | repo root |
| `favicon-16x16.png` | 16×16 | `assets/` |
| `favicon-32x32.png` | 32×32 | `assets/` |
| `apple-touch-icon.png` | 180×180 | `assets/` |
| `favicon.svg` | vector | `assets/` (optional) |

> Free tool to generate all sizes from one image: **https://realfavicongenerator.net**

---

## Print Stylesheet

Link `print.css` in `<head>` — it loads only when printing or saving as PDF:

```html
<link rel="stylesheet" href="print.css" media="print">
```

### print.css rules

```css
/* =============================================
   print.css — Clean black & white, ink-saving
   ============================================= */

@media print {

  /* --- Page setup --- */
  @page {
    margin: 1.5cm 2cm;
    size: A4 portrait;
  }

  /* --- Reset colors to black & white --- */
  * {
    color: #000 !important;
    background: #fff !important;
    box-shadow: none !important;
    text-shadow: none !important;
    border-color: #ccc !important;
  }

  /* --- Typography: use system serif for print --- */
  body {
    font-family: Georgia, 'Times New Roman', serif;
    font-size: 11pt;
    line-height: 1.5;
  }

  h1, h2, h3 {
    font-family: Georgia, serif;
    page-break-after: avoid;
  }

  /* --- Hide screen-only elements --- */
  nav,
  .btn,
  #contact a[href^="mailto"],
  footer,
  .hamburger,
  .open-to-work-badge {
    display: none !important;
  }

  /* --- Show full URLs after links --- */
  a[href]::after {
    content: " (" attr(href) ")";
    font-size: 9pt;
    color: #555 !important;
  }

  /* Skip anchors and # links */
  a[href^="#"]::after,
  a[href^="javascript"]::after {
    content: "";
  }

  /* --- Keep sections together where possible --- */
  section {
    page-break-inside: avoid;
  }

  /* --- Timeline: flatten to simple list --- */
  #experience .timeline-entry {
    border-left: 2px solid #999 !important;
    padding-left: 1em;
    margin-bottom: 1em;
    page-break-inside: avoid;
  }

  /* --- Projects: single column --- */
  #projects .card-grid {
    display: block !important;
  }

  #projects .card {
    border: 1px solid #ccc !important;
    padding: 0.5em;
    margin-bottom: 1em;
    page-break-inside: avoid;
  }

  /* --- Skills tags: inline, minimal --- */
  .skill-tag {
    border: 1px solid #999 !important;
    padding: 0.1em 0.4em;
    margin: 0.1em;
    display: inline-block;
    font-size: 9pt;
  }

  /* --- Hero: condense for print --- */
  #hero {
    min-height: unset !important;
    padding: 1em 0 !important;
  }

  #hero img {
    max-width: 80px !important;
    float: right;
  }

  /* --- Certifications: single column --- */
  #certifications .cert-grid {
    display: block !important;
    columns: 2;
  }
}
```

### Print UX rules for Claude Code

- Every `<section>` must have an `id` attribute matching the nav anchor (e.g. `id="experience"`) — this also enables `page-break-inside: avoid` targeting.
- The `.card-grid`, `.cert-grid`, `.timeline-entry`, and `.skill-tag` class names must be used exactly as specified so `print.css` selectors work without modification.
- Do not use CSS Grid or Flexbox shorthand that can't be overridden — use explicit `display: block` fallbacks in print.

---

## Build Progress

### Completed — 2026-06-25

**Files created / replaced:**

| File | Status | Notes |
|---|---|---|
| `index.html` | ✅ Complete | Full redesign per spec, all placeholders filled from resume |
| `style.css` | ✅ Complete | Warm palette, Playfair Display + Inter, full responsive |
| `script.js` | ✅ Created | Mobile nav toggle, hamburger animation, outside-click close, footer year |
| `print.css` | ✅ Created | Black & white print stylesheet per spec |
| `robots.txt` | ✅ Created | Allows crawlers, blocks AI training bots |
| `sitemap.xml` | ✅ Created | Dated 2026-06-25 |
| `site.webmanifest` | ✅ Created | PWA manifest, cognac theme |
| `assets/resume.pdf` | ✅ Created | Copied from `Michael_Hogan_Resume.pdf` |
| `index.html.bak` | ✅ Backup | Original dark-theme homepage preserved |
| `style.css.bak` | ✅ Backup | Original dark stylesheet preserved |

**Content filled in from `Michael_Hogan_Resume.pdf`:**
- Name: **Michael Hogan** / handle: **tekphreak**
- Hero tagline: Technical Support · Security Operations · Software Development
- About bio: adapted from professional summary; stats: 15+ yrs, 3+ industries, 6+ roles
- Skills: all 5 categories updated to match actual resume competencies
- Experience: all 6 roles with real bullets (PSI Security, Alorica/Verizon, CreSecure, Acculynk, CGS, U.S. Army Signal Corps)
- Contact: `michaelrhogan@gmail.com`, LinkedIn `/michael-r-hogan`, GitHub `/tekphreak`
- JSON-LD schema and all SEO meta tags

**Intentional omissions:**
- Phone number omitted per privacy rules in this spec
- Certifications section **removed** — not present on resume (user decision)
- `cert-grid` class still exists in `print.css` but is harmless if section is absent

**Remaining placeholders in `index.html`:**
- Certifications: section removed; re-add if needed
- `assets/profile.jpg` — user must drop in photo
- Favicon files — user must supply and drop into `assets/` and repo root

**What NOT to change without instruction:**
- `wrangler.jsonc` — Cloudflare Pages deployment config, do not touch
- `404.html` — references `.card` class; pre-existing issue, do not overwrite
- `.bak` files — preserve as rollback option until user approves new design
