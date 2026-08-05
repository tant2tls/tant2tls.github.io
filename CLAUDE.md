# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Tan Ngo's personal academic homepage, deployed on GitHub Pages. It is a **single self-contained `index.html`** — all CSS lives in one `<style>` block in the `<head>`; there is no build step, no framework, no JavaScript beyond a small inline `onerror` avatar fallback. Edits are made directly to `index.html`.

The site's audience is **PhD admissions committees**. Keep the homepage a scannable highlight reel; detailed research/work history is intentionally kept in the CV, not the page. (Research and Experience sections were deliberately removed for this reason — do not re-add them without being asked.)

## Deploy & preview

- **Deploy**: GitHub Pages auto-publishes from the `main` branch (remote `origin` → `github.com/tant2tls/tant2tls.github.io`). Push to `main` and the site is live at `https://tant2tls.github.io` within ~1 minute. There is no CI, test, or lint step — a push is the deploy.
- **Local preview**: open `index.html` directly, or `python -m http.server 8000` from this folder for clean relative-link behavior.

## Adding image assets — verify they are git-tracked

New images are dropped into folders next to `index.html` (`graduation/`, `Qualcomm_AI_Resident/`, and loose files like `avatars_tanngo.jpg`). **These are frequently left untracked by git**, so they render locally but 404 on the live site. After adding any asset and referencing it in `index.html`, always `git add -A` (not just `index.html`) and confirm `git status` shows no untracked image files before pushing.

Reference paths in `index.html` are relative to the repo root (e.g. `graduation/graduation_avatar.jpg`). Note some source filenames contain the misspelling `exellent` — match the actual filename in `src`, but use correct spelling ("Excellent") in visible caption text.

## Page structure & conventions

Sections live in `<section id="...">` blocks; the sticky top nav (`nav.top .links`) anchors to those ids. **When adding or removing a section, update the nav links to match.** Current order: About (`#bio`) → News (`#news`) → Publications (`#publications`) → Systems (`#systems`, "Systems Research Interest") → Residency (`#residency`) → Graduation (`#graduation`) → Education/CV (`#cv`) → Honors → Skills. The `#cv` nav link jumps to the Education section heading, not the PDF; the header contact row has a separate `CV.pdf` link.

Repeatable content is added by copying an existing block:
- **Publication**: copy a `<div class="pub">` block. Author lists bold the site owner as `<b>Tan Van Ngo</b>`; external links go in `.pub-links` as bordered anchor badges.
- **News item**: copy a `<li>` in `.news-list` (a `.date` span + a `.what` span).

Styling is driven by CSS custom properties in `:root` (`--accent: #0b4f9c` is the brand blue, plus `--fg`, `--muted`, `--rule`, `--accent-soft`). Reuse these variables rather than hardcoding colors. Fonts are Inter (body) and Source Serif 4 (headings), loaded from Google Fonts.

## Known content nuances

- Academic ranking is **"one of 4 Excellent Students"** of the graduating class, and the **Director's Certificate of Merit** is likewise given to those **4** outstanding graduates — both use 4 (updated 2026-08-05 from the master `CV.md`). Keep them consistent across bio, News, Education, and Honors.
- The graduation speech is an embedded Facebook video plugin iframe (requires the reel to stay Public) with a plain-link fallback below it for ad-blocked visitors.
- The homepage is the source of truth for what's public; `../CV.md` (one level up, outside this repo) holds the fuller record and is the reference when syncing news/rankings.

## Surrounding application workspace (one level up)

This repo is nested inside `../` (`Tan/`), Tan Ngo's **PhD application workspace** for AI / CS / ML Systems programs — a **separate git repo** with its own history. Commits do not span the two: commit site changes from within this folder, workspace changes from `../`. The homepage is the public highlight-reel cut of the material that lives there:

- `../CV.md` — the **master CV** (detailed record). Add or rewrite CV content there first, then flow it here.
- `../SoP.md` — Statement of Purpose. Its thesis (becoming a researcher who understands AI **end-to-end**, bridging **model design and systems optimization**) is the positioning the whole application ladders up to; keep the homepage's bio and framing aligned with it.
- `../CV_dream/` — untracked scratch space for CV iteration. Pipeline is one direction: `CV.md` → `CV_dream/CV_pdf.md` (concise cut) → `CV_dream/cv.tex` / `cv_v2.tex` (LaTeX renders). The `<!-- ... -->` header comments in `CV_pdf.md` are the authoritative changelog for CV decisions.

**Consistency mandate:** the same facts and metrics appear across `../CV.md`, `../SoP.md`, the CV renders, and this page. Drift between them is a credibility problem for an application. When you change a load-bearing fact, propagate it to every surface in the same session. **Metrics are real — copy them exactly, never round or invent** (e.g. `5.4×` faster eval matched to `1.79e-7` per video; FLUX `2.02 s → 0.86 s`; startup `9 min → ~44 s`). Known drift traps: the graduating-students count (**4**), the LinkedIn handle (`tant2tls` — an old `tanngospring` URL still lingers in places), and the arXiv link for *Track the Noise, Move the World*. Grep across surfaces after touching any of these.

**Producing `CV.pdf`:** the header links to `CV.pdf` in this repo. It is rendered from the LaTeX in `../CV_dream/` (`cd ../CV_dream && pdflatex cv.tex`, or `cv_v2.tex` for the merged research/work layout — both render from `CV_pdf.md`, not `CV.md`). When the CV changes, re-render and copy the PDF here, then `git add CV.pdf` (assets are easily left untracked — see above).
