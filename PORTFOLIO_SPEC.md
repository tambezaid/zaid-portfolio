# Portfolio Website — Zaid Arshad Tambe

> Design & content specification for a single-page portfolio website.
> Use this document to generate or rebuild the site (e.g., with VS Code + an AI assistant), then commit the output to git.

**Live deliverable:** one self-contained `index.html` (HTML + CSS + vanilla JS, no frameworks, no build step).

---

## 1. Overview

| | |
|---|---|
| **Owner** | Zaid Arshad Tambe — Senior Java Developer & Technical Lead |
| **Type** | Single-page personal portfolio |
| **Aesthetic** | Light, premium, modern minimal (Stripe/Linear-grade polish) |
| **Stack** | Plain HTML5 + CSS3 + vanilla JavaScript in one file |
| **Fonts** | [Inter](https://fonts.google.com/specimen/Inter) (400–800) for UI/body, [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) (400–500) for dates/numbers — loaded via Google Fonts |
| **Responsive** | Desktop-first, graceful collapse at 980px / 860px / 760px / 600px / 560px breakpoints |

---

## 2. Design System

### 2.1 Color tokens (CSS custom properties)

```css
:root {
  --bg:          #fbfbfd;   /* page background, near-white       */
  --surface:     #ffffff;   /* cards                              */
  --surface-2:   #f4f5f8;   /* alt section bg, tag chips          */
  --ink:         #16181d;   /* headings, dark panels              */
  --ink-soft:    #4b5161;   /* body text                          */
  --ink-faint:   #8b91a3;   /* captions, meta                     */
  --line:        #e7e9ef;   /* hairline borders                   */
  --indigo:      #4353ff;   /* single accent                      */
  --indigo-deep: #2f3dcc;
  --indigo-soft: #eef0ff;   /* accent tint backgrounds            */
  --shadow-sm: 0 1px 2px rgba(22,24,29,.05), 0 2px 8px rgba(22,24,29,.04);
  --shadow-md: 0 2px 4px rgba(22,24,29,.04), 0 12px 32px rgba(22,24,29,.08);
  --r: 14px;                /* card border radius                 */
  --maxw: 1080px;           /* content max width                  */
  --ease: cubic-bezier(.16,1,.3,1);
}
```

### 2.2 Typography

| Element | Spec |
|---|---|
| H1 (hero) | Inter 800, `clamp(2.6rem, 6.4vw, 4.6rem)`, letter-spacing −.035em, line-height 1.04 |
| H2 (sections) | Inter 700, `clamp(1.7rem, 3.6vw, 2.4rem)`, letter-spacing −.025em |
| Body | Inter 400, 16px, line-height 1.65, color `--ink-soft` |
| Kicker labels | 12px, weight 700, letter-spacing .14em, uppercase, `--indigo`, with a 22px accent dash before |
| Dates / numbers | JetBrains Mono, 12px |
| Bold inline (`<b>`) | weight 600, color `--ink` |

### 2.3 Components

- **Floating pill nav** — fixed, top 16px, horizontally centered. White at 80% opacity + `backdrop-filter: blur(14px)`, 1px `--line` border, fully rounded (100px), `--shadow-sm` (upgrades to `--shadow-md` after scroll). Links are 13px/500 pills that tint `--surface-2` on hover. Last item "Contact" is a solid dark CTA pill (`--ink` bg, white text, hover → `--indigo`).
- **Buttons** — `.btn.primary` (dark bg → indigo on hover, lifts −2px) and `.btn.secondary` (white, 1px border, lifts −2px). 14.5px/600, padding 13px 24px, radius 10px.
- **Cards** — white surface, 1px `--line` border, radius `--r`, `--shadow-sm`; hover → `--shadow-md` + translateY(−2/−3px).
- **Tag chips** — 12.5px/500, `--surface-2` bg, 1px border, radius 7px, padding 4px 11px.
- **Status badge (hero)** — pill with a pulsing green dot (`#28c76f` + soft ring) and text "Technical Lead at InXpress · Mumbai, India".
- **Kicker** — every section opens with `<div class="kicker">Label</div>` then `<h2>` then optional `.sec-sub` paragraph.

### 2.4 Motion

- Hero elements stagger in with a `rise` keyframe (translateY + fade), delays .05s → .4s.
- All sections use a `.reveal` class: `opacity 0 / translateY(22px)` → revealed via `IntersectionObserver` (threshold .08), transition .8s `--ease`, with per-element stagger `(i % 3) * 0.07s`.
- Nav gains stronger shadow on `scrollY > 20`.
- Smooth scrolling: `html { scroll-behavior: smooth }`.
- Selection color: indigo background, white text.

---

## 3. Page Structure (in order)

```
nav            → floating pill navigation
header         → hero
#about         → about + at-a-glance card
#experience    → timeline of 4 roles
#practice      → AI-augmented practice (alt bg --surface-2)
#projects      → White Orchid dark feature card
#skills        → 4 skill cards in 2×2 grid
#recognition   → 3 award cards
#contact       → dark rounded CTA panel
footer         → hairline-top, © line
```

---

## 4. Content (verbatim)

### 4.1 Navigation

Links: About · Experience · AI Practice · Projects · Skills · **Contact** (CTA pill).
At ≤760px hide "AI Practice" and "Skills" links (class `hide-m`).

### 4.2 Hero

- Badge: `● Technical Lead at InXpress · Mumbai, India` (green pulsing dot)
- H1: **Backend systems that turn hard problems into _configuration changes._**
  - "configuration changes." carries a gradient text effect: `linear-gradient(100deg, #4353ff 0%, #7b6cff 60%, #a26bff 100%)` clipped to text.
- Subtitle: *I'm **Zaid Arshad Tambe** — a Senior Java Developer & Technical Lead with **10 years** of experience designing APIs from scratch, decomposing monoliths, and fixing the deep architectural problems that quietly slow teams down for years.*
- Buttons: `View experience` (primary, → #experience) · `Get in touch` (secondary, mailto)
- Decorative: a large soft radial indigo glow behind the hero (`radial-gradient`, ~7% opacity).

### 4.3 About (`#about`)

Two-column grid (1.45fr / 1fr; stacks ≤860px).

**Left** — kicker `About`, H2 **Architecture-first, end to end.**, then three paragraphs:

1. For the last several years my work has been almost entirely on the technical side — API design, monolith decomposition, and integration platforms — leading efforts **from early design through production** alongside architects, product managers, and cross-functional teams.
2. My instinct is to make systems generic where it counts, so adding a new carrier, country, or integration becomes a configuration change rather than another development project. I care about leaving behind **patterns a team can build on consistently**, long after I've moved to the next problem.
3. I've shipped across **logistics, healthcare IT, and financial services** — from global carrier platforms to patent systems used by offices worldwide.

**Right** — "at a glance" card (white, rows divided by hairlines):

| Key | Value |
|---|---|
| Role | Sr. Java Developer · Tech Lead |
| Experience | 10 years |
| Focus | APIs · Integration · Architecture |
| Location | Mumbai, India |
| Education | B.E. Computer Engg · Distinction |
| Email | tambezaid@gmail.com |

### 4.4 Experience (`#experience`)

Kicker `Experience` · H2 **A decade of backend engineering.** · sub: *Four organisations, three industries, one consistent thread: **taking ownership of the hardest architectural problems** and shipping them to production.*

Layout: **vertical timeline** — a 2px `--line` rail on the left with a 16px dot per entry (dot border turns indigo + soft ring on hover); each entry is a white card (hover: lift + `--shadow-md`). Card header row: title left, monospace date right; role line beneath; body paragraph; tag chips.

#### Entry 1
- **Title:** Integration Main Hub · `InXpress India` (company name in indigo)
- **Date:** Feb 2025 — Present · **Role:** Senior Java Developer · Technical Lead
- **Body:** InXpress ran **14 separate codebases** — one per country — for carrier integrations. I led their replacement with a single, configurable REST API platform built from the ground up, now live across all 14 countries. Built the **dynamic endpoint routing engine** and carrier-specific payload transformation layer that make adding a carrier or country a configuration change, not a development project. Defined scalable API patterns with the technical architect, onboarded and mentored developers and QA, and ran sprint ceremonies and stakeholder syncs up to CTO level.
- **Tags:** Java · Spring Boot · REST · AWS · Microservices · Team Leadership

#### Entry 2
- **Title:** LIMS & JPETS · `Trigyn Technologies (IOM)`
- **Date:** Oct 2022 — Jan 2025 · **Role:** Technical Analyst
- **Body:** Lab results took up to five minutes to reach downstream systems on a batch process. I re-architected delivery as a **real-time Spring Boot REST API** — pushing results the moment they're finalised, effectively zero delay — and owned the design end-to-end through Swagger specs and documentation. Integrated LIMS with the NextGen module via **Azure Service Bus** queues and topics. On JPETS, replaced basic auth with **Azure AD client-credential flow**, resolved Fortify findings at the root, and added concurrency controls against simultaneous record edits.
- **Tags:** Spring Boot · Azure Service Bus · Azure AD · Swagger · Security

#### Entry 3
- **Title:** Collateral Platform · `BNP Paribas`
- **Date:** Jan 2022 — Oct 2022 · **Role:** Senior Software Engineer
- **Body:** Designed and built the POC that extracted the Acadia module from the CollWeb monolith into a **standalone, independently deployable service — with zero visible disruption to end users**. Approved and shipped to production, it became the foundation for the platform's move toward microservice-ready deployments. Also replaced a legacy JAR dependency with a Spring REST service, covered production support rota, and ran technical interviews.
- **Tags:** Java · Spring · Monolith Decomposition · CI/CD

#### Entry 4
- **Title:** ePCT & IPAS · `Trigyn Technologies (WIPO)`
- **Date:** Jun 2016 — Jan 2022 · **Role:** Senior Software Engineer
- **Body:** Five and a half years developing and maintaining **ePCT** — the global application patent offices use to manage the Patent Cooperation Treaty process — covering the full cycle from requirements and design through features and unit tests, coordinating directly with the client. Built IP administration modules on **IPAS**.
- **Tags:** Java · JSF · Hibernate · Oracle · JMS

### 4.5 AI-Augmented Practice (`#practice`)

Section background: `--surface-2`.
Kicker `AI-Augmented Practice` · H2 **AI as engineering leverage.** · sub: *AI is a daily part of how I work — not a novelty, but **real leverage across the development lifecycle**. It carries the mechanical effort so my judgment goes where it matters: architecture, trade-offs, and review.*

Four cards in a row (2×2 ≤980px, 1-col ≤560px). Each: a 38px rounded square icon tile (`--indigo-soft` bg, mono number) + title + copy.

| # | Title | Copy |
|---|---|---|
| 01 | Day-to-day coding | Drafting implementations, refactors, and boilerplate quickly — then refining against the patterns the codebase already relies on. |
| 02 | Code review | A first-pass reviewer for diffs, surfacing edge cases and regressions before they reach a human reviewer or production. |
| 03 | Ticket creation | Turning loose requirements into well-scoped JIRA tickets developers and QA can work from without back-and-forth. |
| 04 | Investigations | Tracing integration bugs, payload mismatches, and latency issues — reasoning through logs to reach root cause faster. |

### 4.6 Independent Work (`#projects`)

Kicker `Independent Work` · H2 **Beyond the day job.** · sub: *An end-to-end build delivered independently for a residential construction firm.*

One **dark feature card** — the visual centerpiece:
- Background: `linear-gradient(135deg, #171a2e 0%, #1d2142 55%, #27224d 100%)`, radius 20px, padding 48px, plus a soft radial purple orb glow in the top-right corner.
- Two columns (1.2fr / 1fr; stacks ≤860px).

**Left:**
- Pill tag: `REAL ESTATE · END-TO-END` (purple tint)
- H3 (white, 800): **White Orchid** · sub: *for SM Builders*
- Copy: A complete digital footprint for a residential development: a **public marketing website** for prospective buyers, paired with a **private internal web application** the firm uses to manage its inventory of flats, buyer records, and every detail of a sale — replacing scattered spreadsheets and paperwork with a single source of truth.

**Right** (numbered list, hairline separators):

| # | Item | Copy |
|---|---|---|
| 01 | Public website | Marketing site presenting the development, its units, and project information to buyers. |
| 02 | Internal web application | Staff tool for flat inventory, buyer details, and sale records — one source of truth. |
| 03 | Supporting collateral | QR codes, 3D visualisation, email templates, and print materials. |

### 4.7 Skills (`#skills`)

Kicker `Skills` · H2 **The toolkit.** · sub: *A backend-first stack, shaped by ten years of API and integration work.*

2×2 grid of white cards (1-col ≤760px). Each card: small uppercase header with an 8px indigo square bullet, then tag chips.

| Group | Chips |
|---|---|
| Languages & Frameworks | Java / J2EE, Spring Boot, Spring Core, Hibernate, JPA, JSF, Primefaces, Struts, JUnit, Log4j |
| API & Integration | REST API, Swagger, Azure Service Bus, Azure AD (CCF), AWS S3, AWS EC2, AWS SQS, CloudWatch |
| Architecture | Microservices, Monolith Decomposition, Dynamic Endpoint Routing, Configurable Payload Transformation |
| Databases · Servers · Tooling | Oracle, MySQL, Tomcat, WildFly, Git, JIRA, Bamboo, Maven, Sonar, AI-assisted development |

### 4.8 Recognition (`#recognition`)

Kicker `Recognition` · H2 **Acknowledged along the way.**

Three white cards in a row (1-col ≤860px), each with a 34px round star tile (`--indigo-soft` bg):

1. **Ace Trigynite of the Quarter** — Q2 2023–2024, awarded for outstanding technical contribution.
2. **Academic Excellence** — Certificate awarded in all four years of B.E. (2012–2015).
3. **First Class with Distinction** — B.E. Computer Engineering, University of Mumbai, 2015 (76%).

### 4.9 Contact (`#contact`)

A full-width dark panel: `--ink` background, radius 24px, padding 72px 48px, centered text, soft indigo radial glow at top.

- Kicker (light indigo variant): `Contact`
- H2 (white): **Let's build something that scales.**
- Copy: *Open to conversations about backend architecture, integration platforms, and technical leadership.*
- Buttons: `tambezaid@gmail.com` (white primary → indigo on hover, mailto link) · `+91 87965 08350` (ghost outline, tel link)

### 4.10 Footer

Hairline top border. Left: `© 2026 Zaid Arshad Tambe` · Right: `Senior Java Developer · Mumbai, India`

---

## 5. JavaScript (vanilla, ~15 lines)

```js
// 1. Nav shadow on scroll
const nav = document.getElementById('nav');
addEventListener('scroll', () => nav.classList.toggle('scrolled', scrollY > 20));

// 2. Scroll-reveal
const io = new IntersectionObserver(es => {
  es.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); }
  });
}, { threshold: .08 });
document.querySelectorAll('.reveal').forEach((el, i) => {
  el.style.transitionDelay = (Math.min(i % 3, 2) * 0.07) + 's';
  io.observe(el);
});
```

No dependencies. No build step. No localStorage.

---

## 6. Suggested Repository Setup

```
portfolio/
├── index.html        # the entire site
├── README.md         # this file (or a trimmed version)
└── .gitignore        # optional (e.g., .DS_Store, Thumbs.db)
```

```bash
git init
git add index.html README.md
git commit -m "feat: personal portfolio — light premium single-page site"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

**Free hosting options:** GitHub Pages (Settings → Pages → deploy from `main`), Netlify, or Vercel — all serve a static `index.html` with zero config.

---

## 7. Acceptance Checklist

- [ ] Single `index.html`, no external JS/CSS files (fonts via Google Fonts CDN only)
- [ ] All 9 sections present in order, content matches §4 verbatim
- [ ] Floating pill nav with blur + dark Contact CTA; smooth-scrolls to sections
- [ ] Hero gradient text on "configuration changes.", pulsing badge dot, staggered entrance
- [ ] Experience timeline: rail + dots, hover lift + indigo dot ring
- [ ] White Orchid renders as the dark gradient feature card
- [ ] Scroll-reveal animates every section once
- [ ] Responsive at 980 / 860 / 760 / 600 / 560 px
- [ ] mailto: and tel: links work; selection color is indigo
