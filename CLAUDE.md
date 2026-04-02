# CLAUDE.md

Personal portfolio site for Andre Espinoza. Static HTML, no build tools, deployed to Vercel (andre-espinoza.com via Namecheap nameservers).

## Architecture
- All CSS and JS is inline — no separate files, no bundler
- `index.html` — main portfolio page
- `cartlog.html` — CartLog case study page
- Case study pages follow the same structure as cartlog.html

## Design System (index.html)
- Background: #0a0a0a (ink black)
- Accent: #c9a84c (antique gold)
- Highlight: #c8f135 (acid green)
- Fonts: Unbounded (display), Shippori Mincho (body), IBM Plex Mono (code)
- Custom cursor is desktop-only: gated with `@media (hover: hover) and (pointer: fine)`