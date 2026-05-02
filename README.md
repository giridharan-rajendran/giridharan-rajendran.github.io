# Giridharan Rajendran — Personal Portfolio

Personal portfolio and resume site for **Giridharan Rajendran**, a Senior Engineering Leader based in Everett, WA.

> Live site: <https://giridharan-rajendran.github.io>
> Repo: <https://github.com/giridharan-rajendran/giridharan-rajendran.github.io>

---

## Overview

A single-page portfolio site built with plain **HTML / CSS / vanilla JavaScript**, deployed on **GitHub Pages** with no build step. The site is structured as a tab-driven SPA: all content lives in `index.html` and JavaScript swaps which `<div class="page">` is visible.

Design highlights:

- Dark gradient theme with indigo / violet / sky accents.
- Glassmorphic cards, soft radial-gradient ambient washes, and subtle fade-up scroll animations powered by `IntersectionObserver`.
- Fully responsive (`@media (max-width: 960px)` breakpoints).
- Zero dependencies — no React, no build tools, no `node_modules`.

---

## Project Structure

```text
giridharan-rajendran.github.io/
├── README.md                        ← this file
├── index.html                       ← entire site (HTML + inline CSS + inline JS)
└── giridharan-rajendran-resume.pdf  ← downloadable resume (linked from nav, hero, and contact)
```

That's it. One HTML file, one PDF. No build step, no package manager, no framework.

---

## Pages / Tabs

The SPA exposes seven tabbed sections, each rendered as a `<div class="page">` inside `index.html`:

| Tab          | `id`           | Contents                                                                  |
| ------------ | -------------- | ------------------------------------------------------------------------- |
| Home         | `home`         | Hero banner, stats stack, MBA-in-progress callout, location signal        |
| About        | `about`        | Bio, leadership philosophy, Core Skills + Leadership Competencies bands   |
| Experience   | `experience`   | Full 5-role career timeline back to 2006                                  |
| Projects     | `projects`     | Featured flashcards (DevOps Copilot Hub, CSDM Check) + 4 enterprise inits |
| Achievements | `achievements` | 8 measurable career-impact cards drawn directly from the résumé           |
| Education    | `education`    | Degrees + certifications (MBA, PG Cloud, B.E., RHCE, SAFe, etc.)          |
| Contact      | `contact`      | Live Formspree contact form + direct contact info + resume download       |

> Blog, Talks, and Open Source pages were intentionally removed — they previously contained
> placeholder content. They can be re-added in the future once real articles, talks, or
> public repos exist to back them up.

Tab switching is handled by the `showPage(id)` function (see the inline `<script>` at the bottom of `index.html`).

---

## Featured Project: CSDM Check — Go Implementation

A flagship project showcase built with the "flashcard" layout (`.feat-proj` block):

- **Stack:** Go (single-binary CLI), REST API, Web Dashboard
- **Domain:** Enterprise asset-portfolio querying with full SDLC hierarchy support
- **Compliance:** SOX / PCI / USCGI scanning + GitLab security-policy validation
- **Highlights:** Concurrent API calls, 24-hour smart caching, multi-format output (JSON / CSV / tables), GitLab framework auto-apply

> All corporate names, internal IDs, and product code-names have been **sanitized** to generic public-facing equivalents (e.g. *"a major US carrier"*, *"central asset management system"*, *"APMxxxxxxx"*). Do not re-introduce real names.

A second **Current Project** placeholder card exists for **DevOps Copilot — Hub** (details to be filled in later).

---

## Contact Form (Formspree)

The Contact page hosts a working contact form wired to **Formspree** (the AJAX endpoint flow — no page redirects, inline success/error states).

### How it works

- `<form>` `action` posts to **`https://formspree.io/f/mbdqwojr`**.
- The `handleSubmit(event)` function (in the inline `<script>`) intercepts submission, sends a `fetch` POST with `Accept: application/json`, and shows an inline status:
  - Button cycles `Send Message ✉️` → `Sending…` → `Sent ✓`.
  - Green `.success-msg` banner on HTTP 200; auto-hides after 6 seconds.
  - Red `.error-msg` banner on failure (with mailto fallback to `mr.giridharan.rajendran@gmail.com`).
  - Form `.reset()`s on success.
- **Honeypot** field `_gotcha` is included (invisible to humans, auto-filled by bots — Formspree silently drops those submissions).
- **Subject line** is set via the hidden `_subject` field: *"New message from your portfolio site"*.
- Formspree auto-sets the **`Reply-To`** header to the sender's email, so hitting "Reply" in Gmail goes straight to them.

### What an incoming email looks like

```text
From:     Formspree <noreply@formspree.io>
Subject:  New message from your portfolio site
Reply-To: <sender's email>

Name:         John Smith
Email:        john@company.com
Inquiry Type: Leadership opportunity
Message:
  Hi Giridharan, I'd love to chat about...
```

### Free-tier limits

- **50 submissions / month** on Formspree Free.
- If the cap is hit, additional submissions are paused until the next month resets (sender sees a "form full" message). Upgrade to **Basic** ($10/mo) for 1,000 submissions/month if needed.

### Swapping the endpoint

If the Formspree form ID ever changes, edit one line in `index.html`:

```html
<form id="contactForm" action="https://formspree.io/f/<NEW_FORM_ID>" method="POST" ...>
```

That's the only change required.

---

## Local Development

No build step — just serve the directory with any static file server.

```bash
# Option 1: Python (preinstalled on macOS)
python3 -m http.server 8000

# Option 2: Node (if you have it)
npx serve .

# Then open:
open http://localhost:8000
```

Edit `index.html` directly. Refresh the browser to see changes.

### Testing the contact form locally

1. Run `python3 -m http.server 8000` and open <http://localhost:8000>.
2. Click the **Contact** tab.
3. Fill in name / email / message → click **Send Message ✉️**.
4. Expected: green success banner appears within 1-2 seconds, form clears.
5. Check the Gmail inbox tied to the Formspree account — email should arrive within ~10 seconds.
6. If this is the **first-ever submission** on a new Formspree form, you may receive a one-time *"Confirm your form"* email from Formspree. Click the confirmation link, then test again.

---

## Deployment

The site auto-deploys to GitHub Pages from the `main` branch.

### Workflow used in this repo

1. Day-to-day work happens on the `cursor` branch (or a feature branch).
2. When changes are reviewed and ready, merge `cursor` → `main`.
3. GitHub Pages picks up the change within ~30-60 seconds and republishes <https://giridharan-rajendran.github.io>.

### Push from local

```bash
git add index.html README.md
git commit -m "your message"
git push origin cursor          # push to current branch
# then open a PR to main, or merge locally and push main
```

---

## Recent Changes

### May 2026 — Resume alignment & professional polish

- **SEO + favicon** — added `meta description`, Open Graph + Twitter Card tags, JSON-LD `Person` structured data, and an inline-SVG `GR` gradient favicon.
- **Resume PDF** — copied `giridharan-rajendran-resume.pdf` into the repo so all 4 download buttons (nav / hero / about / contact) actually work.
- **T-Mobile naming** — site now uses the real employer name (matches résumé and LinkedIn) instead of "a major US carrier" anonymization. Internal product code-names other than what's already on the résumé remain redacted.
- **Removed placeholder sections** — Blog, Talks, and Open Source tabs deleted (they had no real backing content). The site now only shows what's verifiable from the résumé.
- **LASON India experience** — added the missing 5th role (May 2006 – Sep 2007) to complete the career timeline.
- **About page** — added a 16-keyword **Leadership Competencies** band drawn from the résumé Core Competencies section (helps recruiters' ATS scans).
- **Home hero** — surfaced **MBA in Progress · Expected 2026** + location/remote-friendly signal.
- **Achievements page** — replaced 6 fabricated awards with 8 real, audited career-impact metric cards drawn straight from the résumé ($1.2M+ saved, 5× deploys, 99.9% uptime, 45% MTTR cut, 800+ hours saved, 25% YoY satisfaction lift, 75% faster reporting, 70% release-cycle reduction).
- **Projects page** — added a clear "Enterprise Initiatives" section header above the 4 internal-T-Mobile project cards. Replaced fake "Live Demo / GitHub" buttons with **measurable-outcome metric chips** + an **"Internal · T-Mobile"** badge so it's clear those systems are proprietary.
- **Calendly booking card** — removed (will be re-added when a personal Calendly account exists).

### April 2026 — Initial build

- **Site architecture** — converted to a single-page tabbed SPA with all CSS / JS inlined in `index.html`.
- **Project showcase** — added "CSDM Check — Go Implementation" with a detailed flashcard layout (capability hierarchy, illustrative examples, key-capabilities checklist, tags).
- **Current project placeholder** — added "DevOps Copilot — Hub" card (details to be filled in later).
- **Data sanitization (CSDM Check)** — removed internal product code-names (e.g. central asset management system instead of MAIA), real APM IDs, and other internal compliance-tooling identifiers from the CSDM Check showcase since these are not on the résumé.
- **Contact form** — wired to Formspree (`https://formspree.io/f/mbdqwojr`) with AJAX submission, honeypot, inline success/error states, and mailto fallback.

---

## Maintenance Checklist

When adding new content:

- [ ] Edit the appropriate `<div class="page">` block in `index.html` (e.g. `#projects` for a new project card).
- [ ] Reuse existing CSS classes where possible (`.feat-proj`, `.tag`, `.chip`, `.glass`, `.fade-up`, etc.) to keep visual consistency.
- [ ] Add `class="fade-up"` to new top-level cards so they pick up the scroll animation.
- [ ] Run `python3 -m http.server 8000` and verify on desktop + mobile widths (DevTools responsive mode, ≤ 960px).
- [ ] Check that no internal company names, real customer names, or non-public IDs leak into copy.
- [ ] Commit on the `cursor` branch, test, then merge to `main` to publish.

---

## Tech Stack

- **HTML5** (semantic structure, single document)
- **CSS3** — CSS variables, linear & radial gradients, `backdrop-filter`, custom properties, media queries
- **Vanilla JavaScript** — `IntersectionObserver` for scroll animations, `fetch` for the Formspree submission, simple `showPage()` tab switcher
- **Google Fonts** — `Inter` (body), `Sora` (display)
- **Formspree** — contact form backend (free tier)
- **GitHub Pages** — hosting

No frameworks. No bundlers. No `node_modules`. Just a single HTML file you can edit and ship.

---

## Contact

- **Email:** [mr.giridharan.rajendran@gmail.com](mailto:mr.giridharan.rajendran@gmail.com)
- **LinkedIn:** <https://linkedin.com/in/giridharan-rajendran>
- **GitHub:** <https://github.com/giridharan-rajendran>
- **Location:** Everett, WA
