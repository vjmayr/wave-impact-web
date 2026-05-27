# MIGRATION PLAN — Inline-Grid → Utility-Klassen (§ 28 waveImpact CSS v3.0)

**Scope:** Alle `*.html` im Projekt-Root mit inline `style="…"`, das SOWOHL `display: grid`
ALS AUCH `grid-template-columns:` enthält. `docs/` ist ausgeschlossen.

**Default-Gap-Konvention:**
`.wi-grid-2` = 32px · `.wi-grid-3` = 24px · `.wi-grid-4` = 32px ·
`.wi-split-*` = 56px · `.wi-split-content-sidebar` = 64px · `.wi-list-icon` = 20px

`gap`-Action: **REMOVE** wenn inline gap = Default; **KEEP** sonst (inline override,
inkl. aller Zwei-Wert-Gaps wie `12px 32px` da diese row-gap ≠ Default haben).

---

## Matched Elements (22)

| # | File | Line | element | grid-template-columns | inline gap | → class | gap action |
|---|------|------|---------|-----------------------|-----------|---------|-----------|
| 1 | waveImpact_expertise.html | 114 | `<div>` Expertise-Felder-Grid | `repeat(4, 1fr)` | `24px` | `.wi-grid-4` | KEEP (24≠32) |
| 2 | waveImpact_expertise.html | 318 | `<div>` Methoden-Grid | `repeat(2, 1fr)` | `24px` | `.wi-grid-2` | KEEP (24≠32) |
| 3 | waveImpact_expertise.html | 439 | `<div>` Sub-Grid in Section | `repeat(3, 1fr)` | `24px` | `.wi-grid-3` | REMOVE (=24) |
| 4 | waveImpact_expertise.html | 473 | `<div>` Aside-Layout (280px Sidebar) | `280px 1fr` | `64px` | `.wi-split-content-sidebar` | REMOVE (=64) |
| 5 | waveImpact_expertise.html | 505 | `<div>` 2-Spalter mit padding+bg | `1fr 1fr` | `16px 32px` | `.wi-grid-2` | KEEP (2-Wert) |
| 6 | waveImpact_kontakt.html | 57 | `<div>` Kontaktkanäle | `repeat(3, 1fr)` | `24px` | `.wi-grid-3` | REMOVE (=24) |
| 7 | waveImpact_kontakt.html | 119 | `<div>` Prozess-Layout | `1.2fr 1fr` | `56px` | `.wi-split-content-aside` | REMOVE (=56) |
| 8 | waveImpact_kontakt.html | 125 | `<li>` Prozess-Item | `56px 1fr` | `20px` | `.wi-list-icon` | REMOVE (=20) |
| 9 | waveImpact_kontakt.html | 136 | `<li>` Prozess-Item | `56px 1fr` | `20px` | `.wi-list-icon` | REMOVE (=20) |
| 10 | waveImpact_kontakt.html | 147 | `<li>` Prozess-Item | `56px 1fr` | `20px` | `.wi-list-icon` | REMOVE (=20) |
| 11 | waveImpact_kontakt.html | 217 | `<div>` Detail-Block | `1fr 1fr` | `56px` | `.wi-grid-2` | KEEP (56≠32) |
| 12 | waveImpact_leistungen_audit.html | 118 | `<ul>` Bullet-Liste | `1fr 1fr` | `12px 32px` | `.wi-grid-2` | KEEP (2-Wert) |
| 13 | waveImpact_leistungen_monitoring.html | 120 | `<ul>` Bullet-Liste | `1fr 1fr` | `12px 32px` | `.wi-grid-2` | KEEP (2-Wert) |
| 14 | waveImpact_leistungen_monitoring.html | 277 | `<ul>` Bullet-Liste | `1fr 1fr` | `16px 40px` | `.wi-grid-2` | KEEP (2-Wert) |
| 15 | waveImpact_leistungen_readiness.html | 117 | `<ul>` Bullet-Liste | `1fr 1fr` | `12px 32px` | `.wi-grid-2` | KEEP (2-Wert) |
| 16 | waveImpact_leistungen_workshops.html | 122 | `<ul>` Bullet-Liste | `1fr 1fr` | `12px 32px` | `.wi-grid-2` | KEEP (2-Wert) |
| 17 | waveImpact_leistungen_workshops.html | 293 | `<ul>` 3er-Bullet-Liste | `1fr 1fr 1fr` | `24px 40px` | `.wi-grid-3` | KEEP (2-Wert) |
| 18 | waveImpact_news.html | 109 | `<div>` News-Cards 3er | `repeat(3, 1fr)` | `32px` | `.wi-grid-3` | KEEP (32≠24) |
| 19 | waveImpact_news.html | 215 | `<div>` News-Cards 3er | `repeat(3, 1fr)` | `24px` | `.wi-grid-3` | REMOVE (=24) |
| 20 | waveImpact_news.html | 260 | `<div>` CTA-Box 2-Spalt | `1fr 1fr` | `64px` | `.wi-grid-2` | KEEP (64≠32) |
| 21 | waveImpact_ueber.html | 233 | `<div>` 2-Spalter-Section | `1fr 1fr` | `32px` | `.wi-grid-2` | REMOVE (=32) |
| 22 | waveImpact_styleguide.html | 151 | `<div class="sg-row">` Beispielzeile | `1fr 1fr` | `64px` | `.wi-grid-2` | KEEP (64≠32) |

---

## Unmatched Patterns (9) — bleiben unverändert

| # | File | Line | grid-template-columns | Grund |
|---|------|------|-----------------------|-------|
| 1 | waveImpact_expertise.html | 235 | `repeat(5, 1fr)` | 5-Spalter nicht in Mapping |
| 2 | waveImpact_expertise.html | 395 | `64px 1fr auto` | 3-Col icon+content+meta nicht in Mapping (`.wi-list-icon` ist nur 2-Col) |
| 3 | waveImpact_expertise.html | 403 | `64px 1fr auto` | s.o. |
| 4 | waveImpact_expertise.html | 411 | `64px 1fr auto` | s.o. |
| 5 | waveImpact_expertise.html | 419 | `64px 1fr auto` | s.o. |
| 6 | waveImpact_expertise.html | 427 | `64px 1fr auto` | s.o. |
| 7 | waveImpact_news.html | 74 | `1.4fr 1fr` | 1.4fr nicht in Mapping (Range 1.1–1.3fr) |
| 8 | waveImpact_ueber.html | 166 | `1.4fr 1fr` | s.o. |
| 9 | waveImpact_ueber.html | 351 | `auto 1fr auto` | 3-Col auto-Layout nicht in Mapping |

---

## Skipped (Rule 2 — kein inline `display: grid`)

Elemente mit `grid-template-columns` inline, aber `display: grid` kommt aus einer Klasse
(z.B. `.wi-services`, `.wi-valueprops`): nicht im Refactor-Scope.

- `waveImpact_leistungen_audit.html:324, 360`
- `waveImpact_leistungen_monitoring.html:322, 358`
- `waveImpact_leistungen_readiness.html:315, 350`
- `waveImpact_leistungen_workshops.html:324`
- `waveImpact_ueber.html:102`

---

## Skipped (Rule 2 — kein `grid-template-columns`)

Elemente mit inline `display: grid` aber ohne `grid-template-columns` (Single-Column-Stack):

- `waveImpact_expertise.html:393`
- `waveImpact_kontakt.html:124, 255`
- `waveImpact_ueber.html:195, 238, 265`

Diese sind außerhalb des Mappings (keine Spalten-Definition).
