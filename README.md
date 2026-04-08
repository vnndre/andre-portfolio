# andre-portfolio

Source for **[andre-espinoza.com](https://andre-espinoza.com)** — Andre Espinoza's personal portfolio.

Hand-coded static HTML, CSS, and vanilla JavaScript. No build step, no framework, no bundler. Deployed to Vercel, domain routed through Namecheap.

## Why it's built this way

Every build tool is a small surrender of control. This portfolio is deliberately the opposite — a single folder of HTML files where the markup, styling, and behavior for each page live together, and the only thing between the code and the browser is Vercel's CDN.

It's also a working design document. The site IS the system — typography, color, motion, and copy voice all live in-file so iterating is a matter of editing one page and refreshing, not wrangling a component tree.

## Structure

```
index.html            main portfolio page — hero, about, project grid
cartlog.html          CartLog receipt scanner case study
holey-moley.html      Holey Moley (Funlab) review analytics case study
topper.html           Topper GPT advising chatbot case study
aventi.html           Aventi travel app — UT McCombs capstone case study
broken-spoke.html     Broken Spoke 360° virtual tour case study
charity-swipe.html    Charity Swipe nonprofit discovery case study
audi.html             Audi brand experience case study
yelp-analysis.html    Yelp data analysis dashboard case study
images/               project screenshots, headshot, hero collage photos
  ig/                 Instagram export photos used in collage hero
CLAUDE.md             design system + architecture notes
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

See `CLAUDE.md` for a deeper breakdown.

## Running locally

```bash
git clone https://github.com/vnndre/andre-portfolio.git
cd andre-portfolio
python3 -m http.server 8000
# → open http://localhost:8000
```

Any static file server works. No dependencies to install.

## Deploy

Pushed to Vercel via the `vercel` CLI. The `.vercel/` project link is git-ignored — use `vercel link` to attach a fresh deploy target if you're forking.

## License

MIT-licensed code — **but the copy, case-study content, photography, and personal branding are not.** If you fork this to build your own portfolio, strip the content out. The project structure, CSS system, and interaction code are yours to adapt.

---

Built by [Andre Espinoza](https://andre-espinoza.com) · [@vnndre](https://github.com/vnndre)
