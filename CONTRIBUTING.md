# Contributing

Corrections, new references, and translations are all welcome — this site is
meant to be maintained in the open.

## How it's built

Plain HTML, generated from Markdown by `build_site.py`. No framework, no JS
build step, no build-time secrets. **Presentation lives entirely in the
external CSS (`assets/css/`) and in the build — never in the content.**

## The one rule that keeps it maintainable

**Write semantic Markdown. Never put inline styles or hand-written HTML in
`content/`.** A pasted `<div style="…">` won't track CSS changes, won't
translate, and punches a hole in the separation that keeps the site
consistent. If Markdown can't express what you need, we add a *token* the build
understands — we don't reach for raw HTML.

## The token vocabulary

Some meaning is carried by tokens the build expands into styled HTML. The main
one is the assessment marker on a load-bearing claim, in descending order of
evidential strength:

- `[[Observed]]`  — directly measured or documented.
- `[[Reported]]`  — a credible field report, not independently verified here.
- `[[Suspected]]` — expected on reasoning or precedent, not yet demonstrated.
- `[[Unexamined]]` — no one has looked closely yet; a named gap, not a claim.

(`[[legend]]` renders the key.) Mark each load-bearing claim with the level it
can actually bear; when in doubt, mark it lower. Want a new construct (a
callout, a figure)? Propose it as a token in an issue — don't inline HTML.

## Anchors and links

Headings, glossary terms, and references each carry a **stable, language-neutral
ID** so links survive edits and translation. Give every heading an explicit ID,
and never rename or translate an ID once it exists:

    ## What is the problem? {#what-is-the-problem}

Cross-page links are root-absolute and localised by the build
(`/faq/#term-…` is rendered as `/en/faq/#term-…`).

## Sourcing

Claims should be checkable against **public** sources. Don't add anything that
isn't publicly citable.

## Translations

Each language lives under its own path (`/en/`, `/pt/`, …). A translation is a
parallel set of files with the **same structure and the same anchor IDs**: you
translate the prose and copy the IDs verbatim. The build checks ID parity.

## Build locally

    python -m venv .venv && source .venv/bin/activate
    pip install -r requirements.txt
    python build_site.py
    python -m http.server -d _site 8000   # http://localhost:8000/

## Pull requests

- For anything substantive, open an issue first so we can agree the change.
- Keep PRs focused; the build must pass (it validates links and anchors).
- Be kind — see `CODE_OF_CONDUCT.md`.

Last updated: 2026-06-22
