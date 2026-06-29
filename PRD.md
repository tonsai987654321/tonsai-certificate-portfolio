# PRD: Tonsai Threetan — Portfolio & Certificate Showcase Site

## Problem Statement

Tonsai Threetan (Automation Engineer / QA) has no public-facing portfolio. His 23 certificates are scattered as local files across multiple folders, and recruiters or collaborators have no single place to see his skills, OSS projects, and credentials.

## Solution

A static single-page portfolio published to GitHub Pages. All certificate images (PDF-converted-to-PNG + native PNG/JPG) are wired into a data-driven cert grid grouped by issuer. No framework needed — plain HTML + CSS + vanilla JS, served from the repo root.

## User Stories

1. As a recruiter, I want to see Tonsai's name, role, and one-line value prop in a large hero, so I can immediately understand who he is.
2. As a recruiter, I want a stat strip (years experience, regression speed-up %, cert count, OSS project count), so I can gauge seniority at a glance.
3. As a hiring manager, I want to click "Résumé ↗" in the nav and open a print-ready résumé in a new tab, so I can download or print it.
4. As a visitor, I want sticky nav links (Work / Certs / Experience / Contact) with smooth scroll, so I can jump between sections without losing context.
5. As a visitor, I want a dark scrolling marquee strip showing all issuer names, so I get a quick visual cue of Tonsai's credential sources.
6. As a recruiter, I want to browse Tonsai's three OSS projects (title, description, tags, repo + live-report links), so I can evaluate hands-on technical depth.
7. As a visitor, I want project rows to invert colours on hover, so the interaction feels intentional and polished.
8. As a visitor, I want certificates grouped under bold issuer headers, so I can find credentials from a specific institution without scanning the whole grid.
9. As a visitor, I want each issuer group to show a cert count, so I know how many credentials exist per issuer without counting cards.
10. As a visitor, I want cert cards to show the actual certificate image, so I can verify authenticity visually.
11. As a visitor, I want cert cards to lift and cast a shadow on hover, so the interaction confirms they are inspectable.
12. As a recruiter, I want to see all 11 active issuer groups including W3Schools, AWS, SET, DSD, ChulaMOOC, and PMP (newly added vs original spec), so I get the full credential picture.
13. As a mobile user, I want the layout to collapse to single-column (stats, cert grid, nav), so the site is usable on my phone.
14. As a visitor, I want to click a large email link in the Contact section, so I can reach Tonsai immediately.
15. As a visitor, I want GitHub, LinkedIn, and phone links in the contact footer, so I have multiple channels to connect.
16. As a developer (Tonsai), I want certificate data in a JS array, so I can add a cert later by editing one object — no HTML surgery.
17. As a developer (Tonsai), I want cert images loaded from a flat `certs/` folder with predictable slug filenames, so I can update images by dropping files without touching HTML.
18. As a developer (Tonsai), I want the accent colour as a single CSS variable `--accent`, so I can rebrand hover states in one line.

## Implementation Decisions

- **Stack**: Single `index.html` with embedded `<style>` and `<script>`. No build tool, no npm, no framework. Fonts via Google Fonts CDN link. Served from repo root for GitHub Pages.

- **Colour tokens**: All design colours implemented as CSS custom properties on `:root` (`--paper`, `--ink`, `--muted-body`, `--label`, `--accent`, `--hairline`, `--card`, etc.). `--accent` defaults to `#0f0f0f`.

- **Certificate data model** — JS array at top of `<script>`:
  ```js
  { id: "coursera-google-it-support", title: "Google IT Support",
    issuer: "Coursera", img: "certs/coursera-google-it-support.png" }
  ```
  A second `ISSUERS` array defines display order and the empty-state flag. Rendering loops `ISSUERS`, filters `CERTS` per issuer, and builds the DOM — no per-cert HTML required.

- **`certs/` folder**: All certificate images copied/renamed from `ton_certificate/` into a flat `certs/` folder at repo root with slug names. Image reference map:

  | Slug | Source |
  |---|---|
  | `coursera-google-it-automation.png` | `Coursera/Coursera_Google IT Automation.png` |
  | `coursera-google-it-support.png` | `Coursera/Coursera_Google IT Support.png` |
  | `coursera-google-data-analytics.png` | `Coursera/Coursera_Google Data Analytics.png` |
  | `coursera-google-project-management.png` | `Coursera/Coursera_Google Project.png` |
  | `coursera-google-ux-design.png` | `Coursera/Coursera_Google UX Design.png` |
  | `datarockie-mini-data-science-bootcamp.png` | `Datarockie/certificate-of-completion-for-mini-data-science-bootcamp-2024.png` |
  | `datarockie-certified-pro-data-analyst.png` | `Datarockie/DataRockie_Professional Data Analyst.png` |
  | `botnoi-data-science-essential-8.png` | `Botnoi/botnoi_data science.png` |
  | `borntodev-github-for-developer.png` | `BORNTODEV/borntodev_GitHub for Developer _certifiacte.png` |
  | `borntodev-chatgpt-for-developer.png` | `BORNTODEV/borntodev_ChatGPT for Developers_certifiacte.png` |
  | `thaimooc-data-science.png` | `ThaiMOOC/Thai MOOC_data_science.png` |
  | `chulamooc-dog-lover.jpg` | `ChulaMOOC/CU_doc lover.jpg` |
  | `pmp-gen-ai-project-managers.png` | `PMP/PMP_Generative AI Overview for Project Managers.png` |
  | `set-ux-certificate.png` | `SET/SET_UX_Certificate.png` |
  | `aws-cloud-practitioner.png` | `AWS/AWS_Cloud Practitioner.png` |
  | `dsd-basic-cybersecurity.png` | `กรมพัฒนาฝีมือแรงงาน/DSD_Basic_Cybersercurity.png` |
  | `w3schools-excel.png` | `W3schools/W3_certificate_of_completion_excel.png` |
  | `w3schools-excel-professional.png` | `W3schools/W3_certificate_of_completion_excel_professional_level.png` |
  | `w3schools-python.png` | `W3schools/W3_certificate_of_completion_python.png` |
  | `w3schools-r.png` | `W3schools/W3_certificate_of_completion_r.png` |
  | `w3schools-sql.png` | `W3schools/W3_certificate_of_completion_sql.png` |
  | `w3schools-sql-professional.png` | `W3schools/W3_certificate_of_completion_sql_professional_level.png` |
  | `w3schools-problem-solving.png` | `W3schools/W3_certificate_of_completion_general_problem_solving_and_logical_reasoning.png` |

- **Issuer order & cert count** (updated from original spec):
  1. Coursera — 5 certs *(Google AI Essentials file not found — omitted)*
  2. DataRockie — 2
  3. Botnoi — 1
  4. BornToDev — 2
  5. ThaiMOOC — 1
  6. ChulaMOOC — 1
  7. PMP — 1
  8. SET — 1
  9. AWS — 1
  10. DSD — 1
  11. W3Schools — 7

  Total: **23 certificates across 11 issuers** (no empty-states — all issuers now have certs).

- **Cert card**: `<article class="cert-card"><div class="cert-thumb"><img src="certs/…" loading="lazy" alt="…"></div><div class="cert-info"><p class="cert-title">…</p></div></article>`. Striped CSS gradient on `.cert-thumb` acts as fallback background if image fails to load.

- **Marquee**: Pure CSS `@keyframes` translating a duplicated list — no JS.

- **Dark sections** (Skills + Contact): Full-bleed background via wrapper `div` with negative margin, not layout disruption.

- **Resume**: `reference/resume.html` copied as `resume.html` to repo root; linked from nav "Résumé ↗" button with `target="_blank"`.

- **Responsive breakpoint at 768px**: stats grid 2×2, cert grid collapses via `auto-fill minmax(196px,1fr)`, nav wraps, all tap targets ≥ 44px.

- **No border-radius anywhere** — intentional brutalist aesthetic per design spec.

- **Hero stats copy**: Update count from "13" to "23" certifications; issuers count updated to "11 active issuers".

## Testing Decisions

Good tests verify visible, external behaviour in a real browser — not implementation details like JS array shape or CSS class names.

**Manual verification checklist (the acceptance test):**
- [ ] All 11 issuer groups render with correct cert counts
- [ ] All 23 cert cards appear under the correct issuer
- [ ] Every cert card shows its real certificate image (no broken images)
- [ ] Hover on project row inverts text/bg colour
- [ ] Hover on cert card lifts with shadow
- [ ] Nav is sticky and has blur backdrop on scroll
- [ ] "Résumé ↗" opens `resume.html` in a new tab
- [ ] All 4 nav anchors smooth-scroll to the correct section
- [ ] Marquee scrolls continuously without jank or gap
- [ ] Mobile ≤768px: no horizontal overflow, single-column cert grid, nav wraps
- [ ] Email `mailto:` link works; GitHub/LinkedIn/phone links correct

No automated test suite — this is a static document, browser inspection is the appropriate seam.

## Out of Scope

- Server-side code, API, database, or contact form submission
- Accent colour switcher UI (variable defined but default hardcoded)
- `reference/Portfolio.dc.html` — not shipped, proprietary runtime, reference only
- Google AI Essentials cert card (no certificate file found)
- Graduation transcripts / accreditation docs (not credentials for display)
- CI/CD pipeline beyond GitHub Pages static deploy

## Further Notes

- **Email**: `tonsai.email@gmail.com` — confirmed in source files.
- **Phone**: `+66 89 770 3251` — from design spec; user should confirm before publish.
- **GitHub handle**: `tonsai987654321` — used in project repo URLs; confirm this matches the real GitHub account.
- **LinkedIn**: `in/tonsai-threetan` — confirm slug is correct.
- **`ChulaMOOC/CU_doc lover.jpg`**: Certificate title is "Dog Lover" — a Chulalongkorn University course on dog care/animal welfare.
- **W3Schools** originally an empty-state in the design spec — now has 7 real certs wired in.
- **AWS** originally an empty-state — now has Cloud Practitioner cert wired in.
- **SET and DSD** are new issuers added at user request beyond the original spec.
- **GitHub Pages deploy**: push `index.html`, `resume.html`, `certs/`, to repo root → Settings → Pages → branch `main` / root.
