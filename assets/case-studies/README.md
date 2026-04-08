# Case Study PDFs

Printable PDF exports of each case study page on [andre-espinoza.com](https://andre-espinoza.com). Useful for:

- Sharing a self-contained case study as an email attachment when a recruiter asks
- Archiving the "current state" of a case study before iterating on the live page
- Accessibility — some reviewers prefer PDF to a scrolling web page

## Generation

PDFs are generated from the live HTML pages using Brave Browser in headless mode:

```bash
/Applications/Brave\ Browser.app/Contents/MacOS/Brave\ Browser \
  --headless --disable-gpu \
  --print-to-pdf=assets/case-studies/cartlog.pdf \
  "file://$PWD/cartlog.html"
```

Any Chromium-based browser (Chrome, Edge, Brave) with `--headless --print-to-pdf` works.

## Status

Empty for now. Will be populated once the v3 portfolio redesign stabilizes — no point printing case studies that are about to change.
