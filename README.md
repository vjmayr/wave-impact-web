# wave-impact-web

Static HTML/CSS templates, brand assets and documentation for the **waveImpact GmbH** website — Responsible AI Consultancy, Bremen, Germany.

## What this is

A complete set of static HTML pages, brand CSS, SVG assets, and project documentation. The templates are designed to be integrated into a WordPress site running the Kadence theme, but they also work as standalone static pages for preview, design reference, or fallback.

## Tech stack

- **HTML5** with semantic markup, no framework dependencies
- **CSS3** with custom properties (CSS variables) — single source of truth in `waveImpact_global.css`
- **SVG** for all brand graphics (logos, hero visual, decorative elements)
- **Native `<details>/<summary>`** for FAQ accordions (no JavaScript runtime needed)
- **WordPress 6.4+** with **Kadence** theme as deployment target

## Repository structure

```
wave-impact-web/
├── README.md                          ← this file
├── .gitignore
├── docs/
│   ├── Website_Handover_2026-05-22.md     ← start here for full project status
│   ├── News_Seite_Setup_Guide.md          ← step-by-step Kadence setup for news page
│   └── Kadence_Integration_Guide.md       ← initial integration notes
├── waveImpact_global.css              ← main stylesheet (22 sections, brand tokens)
├── waveImpact_spacing_overrides.css   ← v1.2 layout-spacing tightening
├── waveImpact_queryloop_bridge.css    ← WordPress Query Loop → waveImpact card styling
├── waveImpact_custom.css              ← supplementary custom styles
├── waveImpact_logo_mark.svg           ← three-wave logo mark
├── waveImpact_logo_horizontal.svg     ← logo mark + wordmark
├── waveImpact_hero_visual.svg         ← hero composition
├── waveImpact_cta_decoration.svg      ← CTA block decoration
├── waveImpact_homepage_reference.html
├── waveImpact_leistungen.html         ← services overview
├── waveImpact_leistungen_readiness.html    ← S1 EU AI Act readiness assessment
├── waveImpact_leistungen_audit.html        ← S2 AI ethics audit & bias testing
├── waveImpact_leistungen_monitoring.html   ← S3 continuous monitoring
├── waveImpact_leistungen_workshops.html    ← S4 responsible AI workshops
├── waveImpact_expertise.html
├── waveImpact_ueber.html
├── waveImpact_news.html               ← news index (static reference; live version is CMS-driven in WP)
├── waveImpact_kontakt.html            ← uses Simply Schedule Appointments + CentralStationCRM embeds
├── waveImpact_impressum.html          ← preliminary — needs attorney review before publishing
├── waveImpact_datenschutz.html        ← preliminary — needs attorney review + Calendly→SSA update
├── waveImpact_styleguide.html         ← kitchen-sink verification page
├── waveImpact_footer.html             ← supplementary
└── waveImpact_timeline.html           ← supplementary
```

## Getting started

### Local preview

Open any HTML file directly in a browser, or start a quick static server:

```bash
cd wave-impact-web
python3 -m http.server 8000
# Open http://localhost:8000/waveImpact_homepage_reference.html
```

All asset paths are relative, so the pages render correctly without further configuration.

### WordPress / Kadence integration

The three CSS files go into Kadence Customizer → Additional CSS, in this order:

1. `waveImpact_global.css` — design system foundation
2. `waveImpact_spacing_overrides.css` — section-spacing fine-tuning
3. `waveImpact_queryloop_bridge.css` — for the News page's Query Loop blocks

HTML templates can be pasted into Custom HTML blocks in the WordPress block editor. The News page uses native Gutenberg Query Loop blocks bridged via the third CSS file — see `docs/News_Seite_Setup_Guide.md` for the complete walkthrough.

## Project status

- ✅ Brand system and CSS architecture complete
- ✅ 12 static HTML page templates complete
- ✅ News page CMS-driven and live in WordPress (Featured + Article Grid Query Loops, 9 categories configured)
- ⏳ Remaining pages awaiting Kadence integration (Leistungen, Expertise, Über, Kontakt, Impressum, Datenschutz)
- ⏳ Legal pages awaiting attorney review
- ⚠️ Datenschutzerklärung still references Calendly — needs update because contact page now uses Simply Schedule Appointments
- ⏳ Six placeholders to fill in legal pages (address, tax ID, phone, insurance, datenschutz@ mailbox, CSCRM AVV)

See `docs/Website_Handover_2026-05-22.md` for the full status snapshot and recommended next steps.

## License & ownership

© 2026 waveImpact GmbH (AG Bremen HRB 42134 HB). All rights reserved. Private repository.

## Contact

Dr. Valentin José Mayr — info@waveimpact.de
