# CLAUDE.md

Personal portfolio site for Andre Espinoza. Static HTML, no build tools, deployed to Vercel (andre-espinoza.com via Namecheap nameservers).

## Architecture
- All CSS and JS is inline — no separate files, no bundler
- `index.html` — main portfolio page
- `cartlog.html` — CartLog case study page
- Case study pages follow the same structure as cartlog.html

## Design System (index.html)
- Background: #050403 (ink black)
- Cream: #ede6d8
- Accent: #c8ff00 (acid green)
- Ember: #ff6030
- Adobe: #c4956a (warm gold)
- Fonts: Syne (display), Crimson Pro (body), JetBrains Mono (code)
- Custom cursor is desktop-only: gated with `@media (hover: hover) and (pointer: fine)`

## Key Features
- **Collage hero** — Instagram photos scattered with parallax scroll, tape decorations
- **Text scramble** — Hero name reveals through character scramble animation (vanilla JS, no GSAP)
- **Magnetic cursor** — `[data-magnetic]` attribute on interactive elements for pull effect
- **About section** — Overlapping photo collage with sticker labels, "currently" cards
- **Project cards** — Scroll-driven expand/collapse via IntersectionObserver
- **Frequency wave** — Canvas-drawn reactive waveform at bottom
- **Grain overlay** — SVG feTurbulence noise texture
- **Glow** — Mouse-following radial gradient

## Images
- `images/` — project screenshots and headshot
- `images/ig/` — Instagram export photos used in hero collage and about section

## Voice/Tone
- Copy is written in Andre's actual voice — deadpan, direct, slightly absurdist
- NOT corporate-creative. "pondering" not "leveraging synergies"
- Personality marquee includes real interests: Techno, Kapital, Glass Beams, Boiler Room, etc.
