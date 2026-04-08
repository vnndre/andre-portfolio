# andre-portfolio

Source for **[andre-espinoza.com](https://andre-espinoza.com)** — Andre Espinoza's personal portfolio.

Static HTML pages with inline CSS and JavaScript. No build step, no framework, no bundler, no separate stylesheets or JS files — every page is a single self-contained `.html`. Deployed to Vercel, domain routed through Namecheap.

Built collaboratively with AI — the design direction, copy, and iteration calls are mine; the code was vibecoded alongside Claude. The repo is how I think about my portfolio as a living document: edit a file, refresh the browser, ship.

## Why it's built this way

One folder of HTML files where the markup, styling, and behavior for each page live together. The only thing between the code and the browser is Vercel's CDN. Iteration is as fast as it gets, and every page is independently editable without touching a build pipeline.

## Structure

```
index.html                main portfolio page — hero, about, project grid
cartlog.html              CartLog receipt scanner case study
holey-moley.html          Holey Moley (Funlab) review analytics case study
topper.html               Topper GPT advising chatbot case study
aventi.html               Aventi travel app — UT McCombs capstone case study
broken-spoke.html         Broken Spoke 360° virtual tour case study
charity-swipe.html        Charity Swipe nonprofit discovery case study
audi.html                 Audi brand experience case study
yelp-analysis.html        Yelp data analysis dashboard case study

images/                   project screenshots, headshot, hero collage photos
  ig/                     Instagram export photos used in collage hero

styles/                   shared CSS (being extracted from inline as of v3)
  design-system.css       colors, fonts, grain, buttons, shared primitives
scripts/                  shared JavaScript (being extracted from inline as of v3)

notes/
  process/                "how I built it" logs for each case study
    cartlog-28-hour-sprint.md
    holey-moley-v1-to-v2.md
    portfolio-redesign-log.md       ← live doc, updated as the site evolves
  prompts/                actual AI prompts behind the tools
    holey-moley-report-prompt.md
    topper-advising-system-prompt.md

assets/
  case-studies/           printable PDF exports of each case study
  research/               interview notes, affinity maps, screeners (anonymized)
  figma/                  public Figma file + prototype share links

CLAUDE.md                 design system + architecture notes
```

## Design system

- **Colors**
  - Background: `#050403` (ink black)
  - Cream: `#ede6d8`
  - Acid green: `#c8ff00`
  - Ember: `#ff6030`
  - Adobe gold: `#c4956a`
- **Typography**
  - Display: [Syne](https://fonts.google.com/specimen/Syne)
  - Body: [Crimson Pro](https://fonts.google.com/specimen/Crimson+Pro)
  - Code: [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)
- **Motion**
  - Text scramble hero name reveal (vanilla JS, no GSAP)
  - Magnetic cursor — `[data-magnetic]` elements pull toward pointer
  - Custom cursor — desktop only, gated with `@media (hover: hover) and (pointer: fine)`
  - Scroll-driven project card expand via IntersectionObserver
  - SVG feTurbulence grain overlay
  - Canvas reactive waveform footer
  - Parallax-scrolled collage hero
- **Voice**
  - Written in Andre's actual voice — deadpan, direct, lowercase energy
  - Not corporate-creative. "pondering" not "leveraging synergies"

See `CLAUDE.md` for a deeper breakdown, and `notes/process/portfolio-redesign-log.md` for the live evolution log.

## Process notes and prompts

The `notes/` directory holds the thinking behind the work, not just the output. Two kinds of docs live there:

- **`notes/process/`** — "how I built it" logs for each major case study, including the pivots I killed, the constraints I worked against, and the decisions that shaped the final design. Good starting points: `cartlog-28-hour-sprint.md` and `holey-moley-v1-to-v2.md`.
- **`notes/prompts/`** — the actual system prompts behind the AI tools in my portfolio, with annotations on why each instruction is there. I'm a UX designer building AI-powered tools, and the prompt is a first-class design artifact. Hiding it would be dishonest.

## Assets

`assets/` holds supporting artifacts that don't belong in the live site but matter to the case studies:

- **`assets/case-studies/`** — printable PDF exports, generated with headless Brave for recruiters who want a self-contained case study they can email or archive.
- **`assets/research/`** — anonymized interview notes, affinity maps, screeners, and research plans.
- **`assets/figma/`** — public Figma share links for the interactive prototypes behind each case study.

## Running locally

```bash
git clone https://github.com/vnndre/andre-portfolio.git
cd andre-portfolio
python3 -m http.server 8000
# → open http://localhost:8000
```

Any static file server works. No dependencies to install — just open the HTML.

## Deploy

Pushed to Vercel via the `vercel` CLI. The `.vercel/` project link is git-ignored — use `vercel link` to attach a fresh deploy target if you're forking.

## License

MIT-licensed code — **but the copy, case-study content, photography, and personal branding are not.** If you fork this to build your own portfolio, strip the content out. The project structure, CSS system, and interaction code are yours to adapt.

---

Built by [Andre Espinoza](https://andre-espinoza.com) · [@vnndre](https://github.com/vnndre)
