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

## Verifikation

```bash
# Erwartet: nur Unmatched (9) + Rule-2-Skips (8) als Treffer
$ grep -nE 'style="[^"]*grid-template-columns' *.html | wc -l
17

# Erwartet: 22 neue Utility-Klassen verteilt auf 9 Files
$ grep -cE 'class="[^"]*wi-(grid-[234]|split-2-1|split-1-2|split-content-aside|split-content-sidebar|list-icon)' *.html
… (Summen: expertise=5, kontakt=6, audit=1, monitoring=2, readiness=1, workshops=2, news=3, ueber=1, styleguide=1)
```
