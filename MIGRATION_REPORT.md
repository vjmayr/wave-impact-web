# MIGRATION REPORT — Inline-Grid → Utility-Klassen

**Run:** 2026-05-27 · **Branch:** workstream-c2-migration
**Scope:** `*.html` im Projekt-Root mit inline `style="…"`, das SOWOHL
`display: grid` ALS AUCH `grid-template-columns:` enthält.

## Summary

- **Files processed:** 9
- **Elements refactored:** 22
- **Unmatched (unverändert gelassen):** 9
- **Skipped (Rule 2 — `display: grid` aus Klasse, nicht inline):** 8

## Replacements pro File

| File | Refactorings | Target-Klassen |
|------|--------------|----------------|
| waveImpact_expertise.html | 5 | `.wi-grid-4` (1), `.wi-grid-2` (2), `.wi-grid-3` (1), `.wi-split-content-sidebar` (1) |
| waveImpact_kontakt.html | 6 | `.wi-grid-3` (1), `.wi-split-content-aside` (1), `.wi-list-icon` (3), `.wi-grid-2` (1) |
| waveImpact_leistungen_audit.html | 1 | `.wi-grid-2` (1) |
| waveImpact_leistungen_monitoring.html | 2 | `.wi-grid-2` (2) |
| waveImpact_leistungen_readiness.html | 1 | `.wi-grid-2` (1) |
| waveImpact_leistungen_workshops.html | 2 | `.wi-grid-2` (1), `.wi-grid-3` (1) |
| waveImpact_news.html | 3 | `.wi-grid-3` (2), `.wi-grid-2` (1) |
| waveImpact_ueber.html | 1 | `.wi-grid-2` (1) |
| waveImpact_styleguide.html | 1 | `.wi-grid-2` (1) |

## Replacements pro Target-Klasse

| Klasse | Count |
|--------|-------|
| `.wi-grid-2` | 11 |
| `.wi-grid-3` | 5 |
| `.wi-grid-4` | 1 |
| `.wi-split-content-aside` | 1 |
| `.wi-split-content-sidebar` | 1 |
| `.wi-list-icon` | 3 |
| `.wi-split-2-1` | 0 |
| `.wi-split-1-2` | 0 |

## gap-Handling

- **gap entfernt** (inline gap = class default): 10 Stellen
  - `.wi-grid-3` mit `gap: 24px` (expertise:439, kontakt:57, news:215)
  - `.wi-split-content-sidebar` mit `gap: 64px` (expertise:473)
  - `.wi-split-content-aside` mit `gap: 56px` (kontakt:119)
  - `.wi-list-icon` mit `gap: 20px` (kontakt:125, 136, 147)
  - `.wi-grid-2` mit `gap: 32px` (ueber:233)
- **gap beibehalten** (inline override): 12 Stellen, davon 6 Zwei-Wert-Gaps
  (`12px 32px`, `16px 32px`, `16px 40px`, `24px 40px`) und 6 Single-Wert-Overrides
  (`24px` auf wi-grid-2/wi-grid-4, `32px`/`56px`/`64px` auf wi-grid-2/wi-grid-3).

## Unmatched Patterns

Diese Elemente entsprechen keinem Eintrag der Mapping-Tabelle und blieben unverändert.

| # | File | Line | grid-template-columns | Element-Kontext |
|---|------|------|-----------------------|------------------|
| 1 | waveImpact_expertise.html | 235 | `repeat(5, 1fr)` | `<div>` 5-spaltiges Sub-Grid (Capability-Cluster). Mapping deckt nur 2/3/4 Spalten ab. |
| 2 | waveImpact_expertise.html | 395 | `64px 1fr auto` | `<article>` Case-Card: Icon-Spalte + Content + Meta-Spalte. 3-Spalter; `.wi-list-icon` ist nur 2-Col. |
| 3 | waveImpact_expertise.html | 403 | `64px 1fr auto` | s.o. (zweite Case-Card) |
| 4 | waveImpact_expertise.html | 411 | `64px 1fr auto` | s.o. (dritte Case-Card) |
| 5 | waveImpact_expertise.html | 419 | `64px 1fr auto` | s.o. (vierte Case-Card) |
| 6 | waveImpact_expertise.html | 427 | `64px 1fr auto` | s.o. (fünfte Case-Card) |
| 7 | waveImpact_news.html | 74 | `1.4fr 1fr` | `<article>` Featured-Top-Story. Mapping deckt nur 1.1–1.3fr 1fr ab. |
| 8 | waveImpact_ueber.html | 166 | `1.4fr 1fr` | `<div>` Story-Block 2-Spalter. s.o. |
| 9 | waveImpact_ueber.html | 351 | `auto 1fr auto` | `<div>` 3-Spalter mit auto-Außenspalten (Avatar + Lead + CTA). Nicht im Mapping. |

**Empfehlung:** Falls diese Muster künftig regelmäßig auftauchen, in § 28 zusätzliche
Klassen ergänzen — z.B. `.wi-grid-5`, `.wi-case-card` (`64px 1fr auto`), `.wi-split-feature`
(`1.4fr 1fr`), `.wi-band-3` (`auto 1fr auto`).

## Skipped (Rule 2 — `display: grid` aus Klasse)

Inline `grid-template-columns` ohne inline `display: grid` (kommt aus Klasse `.wi-services`
oder `.wi-valueprops`) — außerhalb des Refactor-Scopes:

- `waveImpact_leistungen_audit.html:324, 360`
- `waveImpact_leistungen_monitoring.html:322, 358`
- `waveImpact_leistungen_readiness.html:315, 350`
- `waveImpact_leistungen_workshops.html:324`
- `waveImpact_ueber.html:102`

## Verifikation (Phase 1)

```bash
# Erwartet: nur Unmatched (9) + Rule-2-Skips (8) als Treffer
$ grep -nE 'style="[^"]*grid-template-columns' *.html | wc -l
17

# Erwartet: 22 neue Utility-Klassen verteilt auf 9 Files
$ grep -cE 'class="[^"]*wi-(grid-[234]|split-2-1|split-1-2|split-content-aside|split-content-sidebar|list-icon)' *.html
… (Summen: expertise=5, kontakt=6, audit=1, monitoring=2, readiness=1, workshops=2, news=3, ueber=1, styleguide=1)
```

---

# C.2 Extension (CSS v3.1)

**Run:** 2026-05-27 · Auslöser: § 28 ergänzt um `.wi-grid-5`,
`.wi-card-icon-meta` und erweitert `.wi-split-content-aside` auf 1.4fr 1fr.

## Summary

- **Elements refactored (Extension):** 8
- **Verbleibend unverändert:** 1 (bewusst belassen)
- **Combined total (Initial + Extension):** 30 Refactorings über 9 Files

## Refactorings

| # | File | Line | grid-template-columns | inline gap | → class | gap action | weitere Änderungen |
|---|------|------|-----------------------|-----------|---------|-----------|---------------------|
| 1 | waveImpact_expertise.html | 235 | `repeat(5, 1fr)` | `16px` | `.wi-grid-5` | REMOVE (=16) | — |
| 2 | waveImpact_expertise.html | 395 | `64px 1fr auto` | `24px` | `.wi-card-icon-meta` | KEEP (24≠20) | `align-items: center` entfernt (= default) |
| 3 | waveImpact_expertise.html | 403 | `64px 1fr auto` | `24px` | `.wi-card-icon-meta` | KEEP (24≠20) | `align-items: center` entfernt |
| 4 | waveImpact_expertise.html | 411 | `64px 1fr auto` | `24px` | `.wi-card-icon-meta` | KEEP (24≠20) | `align-items: center` entfernt |
| 5 | waveImpact_expertise.html | 419 | `64px 1fr auto` | `24px` | `.wi-card-icon-meta` | KEEP (24≠20) | `align-items: center` entfernt |
| 6 | waveImpact_expertise.html | 427 | `64px 1fr auto` | `24px` | `.wi-card-icon-meta` | KEEP (24≠20) | `align-items: center` entfernt |
| 7 | waveImpact_news.html | 74 | `1.4fr 1fr` | `56px` | `.wi-split-content-aside` | REMOVE (=56) | — |
| 8 | waveImpact_ueber.html | 166 | `1.4fr 1fr` | `64px` | `.wi-split-content-aside` | KEEP (64≠56) | — |

**Note zu #1:** Der ursprüngliche Auftrag erwartete inline `gap: 24px`; tatsächlich war
es `gap: 16px`. Nach Rückfrage bestätigt: Class-Default `.wi-grid-5` = 16px → gap
entfernt (match).

**Note zu #2–#6:** Alle fünf Case-Cards in `expertise.html` haben identische
inline-Definitionen → in einem `replace_all`-Edit migriert.

## Class-Defaults (CSS v3.1, neu/erweitert)

| Klasse | gap | align-items | columns |
|--------|-----|-------------|---------|
| `.wi-grid-5` | `16px` | — | `repeat(5, 1fr)` |
| `.wi-card-icon-meta` | `20px` | `center` | `64px 1fr auto` |
| `.wi-split-content-aside` (erweitert) | `56px` | — | jetzt auch `1.4fr 1fr` |

## Bewusst unverändert (1)

| File | Line | grid-template-columns | Begründung |
|------|------|-----------------------|-----------|
| waveImpact_ueber.html | 351 | `auto 1fr auto` | Einmaliges Pattern (Avatar + Lead + CTA), keine Reuse-Fälle. Inline-Style bleibt; § 24.2 Attribute-Selektoren übernehmen Mobile-Fallback. |

**Bestätigung:** Genau ein Element bleibt mit inline `display: grid` —
`waveImpact_ueber.html:351`. Verifiziert via `grep`.

## Combined Totals (Initial + Extension)

| File | Refactorings | Klassen |
|------|--------------|---------|
| waveImpact_expertise.html | 11 | `.wi-grid-4` (1), `.wi-grid-2` (2), `.wi-grid-3` (1), `.wi-split-content-sidebar` (1), `.wi-grid-5` (1), `.wi-card-icon-meta` (5) |
| waveImpact_kontakt.html | 6 | `.wi-grid-3` (1), `.wi-split-content-aside` (1), `.wi-list-icon` (3), `.wi-grid-2` (1) |
| waveImpact_news.html | 4 | `.wi-grid-3` (2), `.wi-grid-2` (1), `.wi-split-content-aside` (1) |
| waveImpact_ueber.html | 2 | `.wi-grid-2` (1), `.wi-split-content-aside` (1) |
| waveImpact_leistungen_audit.html | 1 | `.wi-grid-2` (1) |
| waveImpact_leistungen_monitoring.html | 2 | `.wi-grid-2` (2) |
| waveImpact_leistungen_readiness.html | 1 | `.wi-grid-2` (1) |
| waveImpact_leistungen_workshops.html | 2 | `.wi-grid-2` (1), `.wi-grid-3` (1) |
| waveImpact_styleguide.html | 1 | `.wi-grid-2` (1) |
| **Summe** | **30** | — |

| Klasse | Combined Count |
|--------|----------------|
| `.wi-grid-2` | 11 |
| `.wi-grid-3` | 5 |
| `.wi-grid-4` | 1 |
| `.wi-grid-5` | 1 |
| `.wi-card-icon-meta` | 5 |
| `.wi-split-content-aside` | 3 |
| `.wi-split-content-sidebar` | 1 |
| `.wi-list-icon` | 3 |

## Verifikation (Extension)

```bash
# Erwartet: genau 1 Treffer (ueber.html:351, bewusst belassen)
$ grep -nE 'style="[^"]*display: grid[^"]*grid-template-columns' *.html
waveImpact_ueber.html:351:      <div style="display: grid; grid-template-columns: auto 1fr auto; …">

# Erwartet: 8 Rule-2-Skips bleiben (display:grid via Klasse, nicht inline)
$ grep -nE 'style="[^"]*grid-template-columns' *.html | wc -l
9   # = 1 belassen + 8 Rule-2-Skips
```

---

# C.2 Extension 2 (CSS v3.2)

**Run:** 2026-05-27 · Auslöser: Default-Gap von `.wi-card-icon-meta`
korrigiert von 20px → 24px (matcht reale Verwendungen). Damit werden die
in Extension 1 als Override beibehaltenen `gap: 24px` auf den fünf
Case-Cards redundant.

## Refactorings

| # | File | Line | Element | Action |
|---|------|------|---------|--------|
| 1 | waveImpact_expertise.html | 395 | `<article class="wi-card-icon-meta">` Case-Card | `gap: 24px;` entfernt (= neuer Default) |
| 2 | waveImpact_expertise.html | 403 | s.o. | `gap: 24px;` entfernt |
| 3 | waveImpact_expertise.html | 411 | s.o. | `gap: 24px;` entfernt |
| 4 | waveImpact_expertise.html | 419 | s.o. | `gap: 24px;` entfernt |
| 5 | waveImpact_expertise.html | 427 | s.o. | `gap: 24px;` entfernt |

Alle fünf Elemente sind identisch → in einem `replace_all`-Edit migriert.
Andere inline-Properties (`padding`, `background`, `border`, `border-radius`)
unverändert.

## Class-Defaults (CSS v3.2, geändert)

| Klasse | Default v3.1 | Default v3.2 | Grund |
|--------|--------------|--------------|-------|
| `.wi-card-icon-meta` gap | `20px` | `24px` | Matcht reale Verwendungen (5/5 Cases hatten Override 24px) |

## Verifikation (Extension 2)

```bash
# Case-Card-Zeilen — erwartet: kein gap inline mehr
$ grep -nE 'wi-card-icon-meta' waveImpact_expertise.html
395:        <article class="wi-card-icon-meta" style="padding: 24px 32px; background: #fff; border: …">
403:        <article class="wi-card-icon-meta" style="padding: 24px 32px; …">
411:        <article class="wi-card-icon-meta" style="padding: 24px 32px; …">
419:        <article class="wi-card-icon-meta" style="padding: 24px 32px; …">
427:        <article class="wi-card-icon-meta" style="padding: 24px 32px; …">

# Verbleibende gap: 24px im File — erwartet: 2 (beide NICHT Case-Card,
# beide bewusst als Override auf wi-grid-4 / wi-grid-2 belassen)
$ grep -nE 'gap: 24px' waveImpact_expertise.html
114:      <div class="wi-grid-4" style="gap: 24px; margin-top: 56px;">
318:      <div class="wi-grid-2" style="gap: 24px; margin-top: 56px;">
```

## Update Combined Totals

Refactoring-Counts unverändert (30) — diese Extension entfernt nur redundante
gap-Overrides, fügt keine neuen Klassenanwendungen hinzu. **gap-entfernt-Bilanz**
wächst von 12 → 17 Stellen.
