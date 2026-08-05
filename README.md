
Thread & Bloom — Landing Page
A fully semantic, responsive single-page site for a small-batch coffee
roastery. No build step, no dependencies — one self-contained HTML file
with embedded CSS, built to demonstrate deliberate CSS layout flow
(normal flow, Flexbox, and Grid) applied section by section.
Project structure
```
.
└── landing-page.html   # everything — markup, styles, and the one SVG illustration
```
Everything lives in one file on purpose: no bundler, no package manager,
no build artifacts to keep in sync. The `<style>` block sits in `<head>`;
there's no external JS.
Inside `landing-page.html`, the CSS is organized into commented blocks
that mirror the page's sections top to bottom:
CSS block	Section	Layout technique
Design tokens (`:root`)	—	custom properties: color, type, spacing scale
`.nav-flow`	Header / nav	Flexbox, `justify-content: space-between`, wraps on narrow screens
`.hero-grid`	Hero	Grid, single column → two columns at `60rem`
`.flow-steps`	Process	Flexbox row → wraps to stacked list on narrow screens
`.origin-grid`	Origins	Grid, `repeat(auto-fit, minmax(16rem, 1fr))` — no media query needed
`.testimonial`	Testimonial (`<aside>`)	normal flow, centered block
`.signup-inner`	Newsletter CTA	Flexbox, wraps form next to copy
`.footer-grid`	Footer	Grid, `repeat(auto-fit, minmax(11rem, 1fr))`
The markup uses real semantic HTML5 landmarks throughout: `<header>`,
`<nav>`, `<main>`, `<section>` (each with `aria-labelledby`), `<article>`
for repeatable origin cards, `<aside>` for the testimonial, `<figure>`/
`<figcaption>` for the SVG illustration, and `<footer>`. Heading levels
step down in order (`h1` → `h2` → `h3`) rather than jumping for visual
size.
Setup
There's nothing to install. Pick whichever of these you have on hand:
Open directly
```bash
open landing-page.html        # macOS
xdg-open landing-page.html    # Linux
start landing-page.html       # Windows
```
Or serve it locally (recommended — some browsers restrict fonts/CSS
loaded from `file://`):
```bash
python3 -m http.server 8000
# then visit http://localhost:8000/landing-page.html
```
or, with Node installed:
```bash
npx serve .
```
Fonts
Type comes from Google Fonts, loaded via `<link>` tags in `<head>`
(Fraunces for display, Inter for body, IBM Plex Mono for labels/data).
This requires an internet connection to render as designed. To work
fully offline, download the three families and swap the `<link>` tags
for local `@font-face` rules — the `--display` / `--body` / `--mono`
custom properties in `:root` are the only place font names are
referenced, so that's the only spot to edit.
Responsive behavior
There are two real breakpoints, both `min-width` (mobile-first):
`60rem` — hero switches from stacked to a two-column grid
`44rem` — the connecting line behind the process steps hides (the
steps themselves already wrap via Flexbox at any width)
Everything else — the origin cards, the footer columns, the nav links —
reflows on its own via `auto-fit`/`wrap` rather than fixed breakpoints,
so it holds up at arbitrary widths, not just common device sizes.
Editing content
All copy is hardcoded in the markup — there's no CMS or data file. Swap
text directly in `landing-page.html`. The three origin `<article>` cards
under `id="origins"` and the four `<li class="flow-step">` items under
`id="process"` are the two places that repeat a pattern, so add or
remove a card/step by copying an existing sibling.
