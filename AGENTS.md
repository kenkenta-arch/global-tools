# Global Tools — instructions for Codex

A free, no-signup collection of small browser tools for an **English-speaking, worldwide audience**.
Static HTML/CSS/JS only (no build step, no server). Published with GitHub Pages.
The owner is not a programmer. They only review and merge pull requests on their phone.
**Write pull request descriptions in Japanese** (short and simple). Everything on the site itself is in English.

This is the English sister project of a Japanese tool site run separately. Do not copy its Japanese text; write natively for English users.

## Goal
- Add **1 high-quality tool per task** that real people search for in English.
- Revenue later comes from display ads (Google AdSense) once there are ~15 tools and some traffic. Do not add ads yet.

## When asked to "add a tool"
1. Pick the first unchecked idea in `ideas.md`. If none fit, research: find an English search need where the top results are slow, ad-heavy, or bad on mobile. Prefer long-tail needs (e.g. "pity calculator", "resin refill time") over saturated ones (e.g. "BMI calculator").
   - Avoid topics where a mistake could seriously hurt users (medical dosage, legal advice, tax filing) unless you can cite an official source on the page.
2. Create `tools/<english-slug>/index.html`, following the structure of existing tools.
   - `<title>` and `<meta name="description">` must contain the words people actually search for.
   - Each tool page must include a **"How to use"** section and an **"FAQ"** section with original text (good for search).
   - Respect international users: offer unit switches where relevant (metric / imperial), use the browser locale for number and date formatting, and never assume a country unless the tool is country-specific (say so in the title).
   - Keep a placeholder `<div class="ad-slot"><!-- AD_SLOT --></div>`.
   - **Never send user input anywhere.** Everything runs in the browser.
3. Test with Playwright:
   - Check results against an independent calculation (e.g. compute the expected answer in Python and compare).
   - Try edge cases: empty input, 0, negative numbers, very large numbers, invalid files.
4. Pre-publish checklist (fix until all pass):
   - [ ] Screenshot at 375px width: no cut-off text, no horizontal scroll, buttons easy to tap
   - [ ] No console errors
   - [ ] Title and description contain real search terms
   - [ ] "How to use" and "FAQ" are present and original
   - [ ] No user data leaves the browser
   - [ ] Money/health/legal topics have a clear disclaimer
   - [ ] Any open-source code used is listed in `credits.html` with its license
   - [ ] **No trademarks in the tool name or title** (e.g. don't name a tool after a specific game or brand). Generic wording is fine: "Gacha Pity Calculator", not "<Game name> Pity Calculator". You may mention compatibility in the body text.
5. Add the tool to `index.html` and `sitemap.xml`, and add one line to `log.md`.
6. Commit to a branch `tool/<slug>`, push, and open a pull request to `main`.
   - PR description (Japanese): what the tool does, target English search terms, open-source used and license, how you tested it, and "問題なければMergeを押すと公開されます".
   - If another open `tool/` PR conflicts with `main`, merge `main` into that branch and resolve. **Never force-push.**

## First task (set up the site) — do this before adding tools
- `index.html` (tool list), `style.css` (clean, light + dark mode, mobile first), `privacy.html` (input never leaves the browser; future ads/cookies notice including Google's standard wording and opt-out links; disclaimer), `about.html` (no personal names), `credits.html`, `sitemap.xml`, `robots.txt`, `log.md`, `ideas.md`.
- Pick a short, original site name (check it is not an existing brand). Put it in the header and footer.
- Footer on every page: links to About, Privacy, Credits.

## Open-source rules
- Only MIT / Apache-2.0 / BSD licensed code. No GPL, no code without a license.
- Prefer vendoring a pinned file (e.g. `vendor/pdf-lib-1.17.1.min.js`) over a CDN. If a CDN is used, pin the exact version.

## Things not to do
- No sign-ups, no tracking scripts, no analytics beyond Google Search Console.
- No auto-generated filler articles. Each page must be a working tool with genuinely helpful text.
- Don't put the owner's real name, school, or location anywhere in the repository.
