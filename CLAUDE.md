# Best Mortgage Calculator Ever — project context

A free, client-side mortgage calculator deployed on GitHub Pages at
**https://honestmortgagemath.com**. All math runs in the browser (vanilla JS +
inline SVG charts) — no build step, no framework, no backend. Every calculation
is covered by an in-page self-test panel (26 tests, all green).

## Repo layout
- `index.html` — the **entire app** (HTML + CSS + JS in one ~130 KB file). Source of truth; edit here.
- `<tool>-calculator/index.html` — 6 static SEO landing pages that deep-link into the app via `?tool=<id>`:
  `refinance-calculator/`, `mortgage-recast-calculator/`, `biweekly-mortgage-calculator/`,
  `mortgage-points-calculator/`, `rent-vs-buy-calculator/`, `mortgage-affordability-calculator/`.
- `assets/` — shared images. `og-image.png` — 1200×630 social card.
- `CNAME` — custom domain. `robots.txt`, `sitemap.xml` — SEO.

## The 9 in-app tools (tab ids)
`calc` Calculator · `afford` Affordability · `compare` Compare · `refi` Refinance ·
`points` Points · `recast` Recast · `biweekly` Biweekly · `rentbuy` Rent vs Buy · `arm` ARM.
Tabs switch client-side (URL stays `/`); `?tool=<id>` opens a specific tab on load.

## Conventions
- Keep everything in `index.html`. Match the existing token-based CSS: `--accent` (teal) = principal,
  `--cost` (coral) = interest. Support both light and dark themes via the token pattern.
- Money math lives in the FINANCE ENGINE block (`pmt`, `buildSchedule`, reverse-solve helpers).
  Reuse it — never duplicate formulas.
- Text inputs go inside `.in-wrap` (the `.in-wrap input` selector gives full width + the box styling).
- Every new financial tool MUST add rows to a `runVerification*` function. Ship only with all tests green.
- Match the surrounding code's density/idiom. No new dependencies.

## Deploy (edit → commit → push → live in ~1 min)
1. Edit `index.html` (or a landing page).
2. `git add -A && git commit -m "..." && git push origin main`.
3. GitHub Pages rebuilds; live at honestmortgagemath.com in ~60–90s.
4. Verify: load the site, confirm the self-test pill reads "N/N passing" and no console errors.
- `gh` CLI: `C:\Program Files\GitHub CLI\gh.exe` (authenticated).
  Build status: `gh api repos/JohnThomasGrossi/best-mortgage-calculator/pages/builds/latest --jq .status`
- Note: on Windows PowerShell, `git push` prints progress to stderr and shows as a red
  NativeCommandError even on success — look for the `main -> main` line.

## Domain / DNS
Registered + DNS at Cloudflare. Apex `A` records → GitHub Pages (185.199.108–111.153),
`www` CNAME → johnthomasgrossi.github.io, all **DNS-only (grey cloud)** so GitHub can issue
the TLS cert. "Enforce HTTPS" is on. Do not enable the Cloudflare proxy without switching
SSL/TLS mode to Full (see the Drive hub).

## Plan, status & sensitive reference
Human-facing plan, current status, account/DNS reference, and the SEO/monetization roadmap
live in Google Drive: **`G:\My Drive\Honest Mortgage Math\`** — read `STATUS.md` there first.
Keep account emails / DNS details OUT of this public repo.

## Guardrails
Keep the "not financial advice" disclaimer. Never fabricate ratings/reviews in JSON-LD.
