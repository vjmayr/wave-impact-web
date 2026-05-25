# News-Seite in Kadence: Komplette Setup-Anleitung

**Stand:** 22. Mai 2026
**Voraussetzungen:** WordPress 6.4+, Kadence Theme, alle waveImpact-CSS-Dateien eingebunden.

Diese Anleitung führt Sie von einer leeren News-Seite zur vollständigen, CMS-driven Veröffentlichungsstruktur. Sechs Sektionen werden angelegt: vier statische (Hero, Themensäulen-Pills, Newsletter-Signup, Final CTA) und zwei dynamische (Featured Article, Article Grid). Die statischen Sektionen sind Custom-HTML-Blöcke; die dynamischen sind Gutenberg-Query-Loop-Blöcke.

---

## Teil A — Vorbereitung außerhalb des Seiten-Editors

### A.1 — Die neun Kategorien anlegen

WP-Admin → Beiträge → Kategorien. Für jede der neun Themensäulen:

| Name | Slug | Beschreibung |
|------|------|--------------|
| EU AI Act | `eu-ai-act` | Pflichten, Fristen und Risikoklassen der EU-KI-Verordnung — eingeordnet für werteorientierte Mittelständler. Was bis wann gilt, wer betroffen ist und wo die größten Stolpersteine liegen. |
| ISO 42001 & Normen | `iso-42001-normen` | ISO/IEC 42001 als erwartete harmonisierte Norm für die AI-Act-Konformität, plus Bezüge zu ISO 27001, 9001 und sektorspezifischen Standards. Was die Norm leistet, was sie nicht leistet, wo sie operativ greift. |
| Fairness & Bias | `fairness-bias` | Methodische Beiträge zur Erkennung, Messung und Mitigation von Bias in KI-Systemen. Statistische Parität, Equalized Odds, intersektionale Analysen — und warum einmalige Audits nicht reichen. |
| Erklärbarkeit & Transparenz | `erklaerbarkeit-transparenz` | Explainable AI in der Praxis: SHAP, LIME, kontrafaktische Erklärungen und technische Dokumentation nach Annex IV. Was Erklärbarkeit für Behörden, Aufsichtsräte und betroffene Personen tatsächlich leisten muss. |
| KI-Monitoring | `ki-monitoring` | Drift-Detection, Fairness-Creep, Post-Market-Monitoring nach Art. 72 EU AI Act. Wie sich KI-Systeme über die Zeit verändern — und welche kontinuierlichen Prüfprozesse Compliance und Verantwortung sichern. |
| KI-Governance & Strategie | `ki-governance-strategie` | Strategische Ebene: KI-Inventar, Risikoklassifizierung, Verantwortlichkeiten in der Geschäftsführung, AI Procurement und Make-or-Buy-Entscheidungen. Wie Mittelständler KI-Governance strukturell verankern. |
| KI & Mensch | `ki-mensch` | KI-Einsatz aus Workforce-Perspektive: Arbeitsplatz-Auswirkungen, Mitbestimmung, AI Literacy, Change Management. Wo werteorientierte Personalpolitik und algorithmische Praxis zusammentreffen. |
| KI & Nachhaltigkeit | `ki-nachhaltigkeit` | Der unsichtbare ökologische und soziale Fußabdruck von KI: CO₂, Wasser, Scope 3, ESRS E1. Wie KI in den Nachhaltigkeitsbericht kommt und wo CSRD-Pflichten beginnen. |
| GenAI & LLMs | `genai-llms` | Foundation Models, GPAI nach EU AI Act, Multi-Agent-Systeme. Die spezifischen Risiken generativer KI — Halluzination, Datenleckage, IP-Themen — und wie sich werteorientierte Unternehmen dazu positionieren. |

### A.2 — Mindestens einen Sticky Post anlegen

Damit Sie die Featured-Sektion testen können:

1. WP-Admin → Beiträge → Erstellen
2. Titel und Inhalt schreiben (z.B. einen der bestehenden Anker-Artikel)
3. Rechte Seitenleiste → Reiter „Beitrag" → Abschnitt „Status & Sichtbarkeit"
4. Checkbox **„Diesen Beitrag oben halten"** aktivieren
5. Kategorie zuweisen (z.B. „KI & Nachhaltigkeit")
6. Auszug pflegen (rechte Seitenleiste → „Auszug" → 30–60 Wörter)
7. Beitrag veröffentlichen

Optional zwei oder drei weitere Beiträge ohne Sticky-Status anlegen, damit auch der Article-Grid-Bereich getestet werden kann.

### A.3 — CSS-Dateien prüfen

In Kadence Customizer → Zusätzliches CSS müssen folgende Inhalte (in dieser Reihenfolge) hinterlegt sein:

1. Inhalt von `waveImpact_global.css`
2. Inhalt von `waveImpact_spacing_overrides.css` (v1.2)
3. Inhalt von `waveImpact_queryloop_bridge.css`
4. **Plus** die :has()-Erweiterung für das forcierte Grid-Layout:

```css
.wp-block-post-template:has(.wi-article-card) {
  display: grid !important;
  grid-template-columns: repeat(3, 1fr) !important;
  gap: 32px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.wp-block-post-template:has(.wi-article-card) > li {
  list-style: none;
  margin: 0;
}

@media (max-width: 1024px) {
  .wp-block-post-template:has(.wi-article-card) {
    grid-template-columns: repeat(2, 1fr) !important;
  }
}

@media (max-width: 640px) {
  .wp-block-post-template:has(.wi-article-card) {
    grid-template-columns: 1fr !important;
  }
}
```

---

## Teil B — Die News-Seite anlegen

### B.1 — Neue Seite erstellen

1. WP-Admin → Seiten → Erstellen
2. Titel: `News`
3. URL-Slug: `news` (automatisch aus Titel generiert)
4. Vorlage rechts: „Default" oder „Full Width" (in Kadence)
5. Noch nicht speichern — wir bauen erst die Sektionen

### B.2 — Listenansicht aktivieren

Im Editor oben links auf das **Listenansicht-Icon** (drei horizontale Linien) klicken. Die Listenansicht ist ab jetzt Ihr wichtigstes Navigations-Werkzeug. Lassen Sie sie permanent geöffnet.

---

## Teil C — Hero-Sektion (statisch)

### C.1 — Custom HTML Block einfügen

1. Block-Inserter `+` öffnen oder `/html` tippen
2. **„Custom HTML"** auswählen
3. Folgendes HTML einfügen:

```html
<section class="wi-section">
  <div class="wi-container">
    <p class="wi-eyebrow">News &amp; Blog</p>
    <h1 class="wi-display" style="margin-top: 20px; max-width: 22ch;">
      Substanz statt Marketing.
    </h1>
    <p class="wi-lead" style="margin-top: 28px; max-width: 60ch;">
      Hier veröffentlichen wir Artikel, die für unsere Beratungsarbeit
      relevant sind — und für werteorientierte Unternehmen, die KI
      verantwortungsvoll einsetzen wollen. Frei zugänglich, ohne
      Lead-Magnet-Trichter, ohne Tracking. Eine Veröffentlichungs­tradition,
      die zu unserem Anspruch an Beratung passt: Wer Vertrauen verkauft,
      muss seine Arbeit prüfbar machen.
    </p>
  </div>
</section>
```

4. Block-Vorschau (Eye-Icon in der Toolbar) → prüfen, dass die Überschrift erscheint

### Checkpoint C
✓ Hero erscheint mit großer Überschrift „Substanz statt Marketing." und Lead-Text darunter.

---

## Teil D — Themensäulen-Pills (statisch)

### D.1 — Neuer Custom HTML Block unterhalb der Hero-Sektion

1. Cursor unter den Hero-HTML-Block setzen, `+` klicken
2. „Custom HTML" auswählen
3. Folgendes HTML einfügen (URLs zeigen auf die Category-Archive-Seiten):

```html
<section class="wi-section" style="padding-block: 48px 0; border-top: none;">
  <div class="wi-container">
    <div style="display: flex; gap: 10px; flex-wrap: wrap; align-items: center;">
      <span style="font-size: 12px; font-weight: 700; letter-spacing: 0.14em; color: var(--wi-text-muted); text-transform: uppercase; margin-right: 8px;">Themensäulen:</span>
      <a href="/news" style="display: inline-block; padding: 8px 16px; background: var(--wi-green); color: #fff; border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">Alle Artikel</a>
      <a href="/category/eu-ai-act/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">EU AI Act</a>
      <a href="/category/iso-42001-normen/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">ISO 42001 &amp; Normen</a>
      <a href="/category/ki-governance-strategie/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">KI-Governance &amp; Strategie</a>
      <a href="/category/fairness-bias/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">Fairness &amp; Bias</a>
      <a href="/category/erklaerbarkeit-transparenz/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">Erklärbarkeit &amp; Transparenz</a>
      <a href="/category/ki-monitoring/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">KI-Monitoring</a>
      <a href="/category/genai-llms/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">GenAI &amp; LLMs</a>
      <a href="/category/ki-mensch/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">KI &amp; Mensch</a>
      <a href="/category/ki-nachhaltigkeit/" style="display: inline-block; padding: 8px 16px; background: #fff; color: var(--wi-text); border: 1px solid var(--wi-border); border-radius: 999px; font-size: 13px; font-weight: 700; text-decoration: none; line-height: 1.4;">KI &amp; Nachhaltigkeit</a>
    </div>
  </div>
</section>
```

### Checkpoint D
✓ Unter dem Hero erscheint eine Pill-Reihe mit „Alle Artikel" in Grün und neun weiteren Pills in weißem Rahmen.

---

## Teil E — Featured Article (Query Loop 1)

Dies ist der dynamische Bereich, der den Sticky Post hervorgehoben anzeigt. Der gesamte Bereich wird in drei Sub-Sektionen aufgebaut: ein Heading-Wrapper, dann der Query Loop selbst.

### E.1 — Heading-Sektion einfügen

Neuer Custom HTML Block:

```html
<section class="wi-section">
  <div class="wi-container">
    <p class="wi-eyebrow">Aktueller Artikel</p>
    <h2 class="wi-h2" style="margin-top: 16px; margin-bottom: 32px; max-width: 32ch;">
      Der neueste Beitrag aus dem waveImpact-Blog.
    </h2>
    <!-- Query Loop kommt direkt darunter -->
  </div>
</section>
```

**Wichtig:** Das schließende `</section>` und `</div>` müssen vorerst weggelassen werden, weil der Query-Loop-Block dazwischen kommen muss. Das HTML soll vorerst „offen" enden.

Alternativ und sauberer:
1. Den HTML-Block oben mit allen Tags inklusive schließendem `</section></div>` einfügen
2. Den Query-Loop-Block UNTERHALB einfügen (in eigener wi-section)

Der zweite Ansatz ist robuster — er erspart Probleme mit nicht geschlossenen Tags. Verwenden Sie die zweite Variante:

```html
<section class="wi-section" style="padding-block: 64px 32px;">
  <div class="wi-container">
    <p class="wi-eyebrow">Aktueller Artikel</p>
    <h2 class="wi-h2" style="margin-top: 16px; margin-bottom: 0; max-width: 32ch;">
      Der neueste Beitrag aus dem waveImpact-Blog.
    </h2>
  </div>
</section>
```

### E.2 — Query-Loop-Block einfügen

1. Unter dem Heading-HTML-Block: Block-Inserter `+` oder `/query` tippen
2. **„Query Loop"** auswählen
3. Es erscheint ein Auswahlbildschirm: **„Choose"** vs. **„Start blank"**
4. **„Start blank"** klicken
5. Aus den vier Basis-Varianten **„Title, Date & Excerpt"** wählen

Die Standard-Struktur erscheint im Editor. In der Listenansicht sehen Sie jetzt:

```
Query Loop
├── Post Template
│   ├── Post Title
│   ├── Post Date
│   └── Post Excerpt
└── Pagination
```

### E.3 — Query Loop konfigurieren

1. In der Listenansicht den **äußersten** „Query Loop"-Block anklicken
2. Rechte Seitenleiste → Reiter **„Einstellungen"** (Zahnrad-Icon)
3. Folgende Werte setzen:
   - **Beitragstyp / Post Type**: Beiträge
   - **Sortierreihenfolge**: Neueste zuerst (Datum, absteigend)
   - **Elemente pro Seite**: `1`
   - **Versatz**: `0`
   - **Filter** ausklappen → **Sticky-Beiträge**: **„Only sticky posts"** wählen *(in manchen WP-Versionen heißt diese Option „Show only" oder ist unter „Erweiterte Filter" zu finden)*

### E.4 — Pagination entfernen

Bei nur einem Item brauchen wir keine Pagination.

1. In der Listenansicht den **„Query Pagination"**-Block auswählen
2. Block-Toolbar → 3-Punkte-Menü → **„Block entfernen"**

### E.5 — Inhalt im Post Template gruppieren ⚠️ KRITISCH

Dies ist der entscheidende Schritt, ohne den die Karten-CSS nicht greift.

1. In der Listenansicht den **„Post Template"**-Block ausklappen (kleiner Pfeil davor klicken)
2. Die drei Kind-Blöcke nacheinander mit `Strg+Klick` (Windows) bzw. `Cmd+Klick` (Mac) markieren:
   - Post Title
   - Post Date
   - Post Excerpt
3. **Alle drei sind jetzt mehrfach-markiert** (erkennbar an blauen Rahmen um jeden Block)
4. In der Block-Toolbar (erscheint oben) das **3-Punkte-Menü** öffnen
5. **„Gruppieren"** auswählen *(in manchen WP-Versionen unter „Transformieren in" → „Gruppe")*

Die Struktur in der Listenansicht ist jetzt:

```
Query Loop
└── Post Template
    └── Group ← NEU
        ├── Post Title
        ├── Post Date
        └── Post Excerpt
```

### E.6 — CSS-Klasse für den Group-Block setzen

1. Den **Group**-Block in der Listenansicht auswählen
2. Rechte Seitenleiste → Reiter **„Block"** *(nicht „Einstellungen")*
3. Ganz unten den Abschnitt **„Erweitert"** ausklappen
4. Im Feld **„Zusätzliche CSS-Klasse(n)"** exakt eintragen:

```
wi-featured-article
```

Keine Anführungszeichen, kein Punkt davor, kleingeschrieben, mit Bindestrich.

### E.7 — Post-Categories ergänzen

1. In der Listenansicht den Group-Block aufklappen
2. **Oberhalb von Post Title** einen neuen Block einfügen:
   - Cursor in Post Title setzen → Tastenkombination `Enter` am Anfang der Zeile drückt einen neuen Block oberhalb ein
   - Alternativ: `+` in der Toolbar zwischen den Blöcken
3. Block-Inserter → suchen nach **„Post Terms"** → einfügen
4. Den Post-Terms-Block selektieren
5. Rechte Seitenleiste → „Einstellungen" → **Taxonomie**: **„Kategorien"** auswählen
6. Falls eine Trennzeichen-Option erscheint: leer lassen oder Punkt setzen

In der Listenansicht jetzt:

```
Group [wi-featured-article]
├── Post Terms ← NEU (Kategorien)
├── Post Title
├── Post Date
└── Post Excerpt
```

### E.8 — Read-More-Block ergänzen

1. **Unterhalb von Post Excerpt** einen neuen Block einfügen
2. Block-Inserter → suchen nach **„Weiterlesen"** oder **„Read More"** → einfügen
3. Den Read-More-Block selektieren
4. Linktext anpassen: in der Block-Toolbar oder per Klick direkt im Block → Text ändern zu z.B. **„Artikel lesen"**

In der Listenansicht final:

```
Group [wi-featured-article]
├── Post Terms (Kategorien)
├── Post Title
├── Post Date
├── Post Excerpt
└── Read More (Artikel lesen)
```

### E.9 — Post Title als Link aktivieren

1. **Post Title**-Block auswählen
2. Rechte Seitenleiste → „Einstellungen"
3. Toggle **„Titel zum Beitrag verlinken"** aktivieren

Damit wird die Überschrift im finalen Output als `<a href="...">` gerendert.

### Checkpoint E

1. Seite speichern (oben rechts „Aktualisieren")
2. Vorschau in neuem Tab öffnen
3. Prüfen:
   - ✓ Der Sticky-Post erscheint mit hellem Hintergrund (Surface-Soft)
   - ✓ Kategorien-Pill in Grün
   - ✓ Großer Titel, klickbar
   - ✓ Datum und Excerpt darunter
   - ✓ „Artikel lesen →"-Button in Grün, prominent

Falls etwas nicht stimmt: siehe Troubleshooting-Sektion am Ende.

---

## Teil F — Article Grid (Query Loop 2)

Die Schritte spiegeln Teil E, mit drei Unterschieden in der Konfiguration. Schritte ohne Abweichung sind verkürzt beschrieben.

### F.1 — Heading-Sektion einfügen

Neuer Custom HTML Block unter dem Featured-Query-Loop:

```html
<section class="wi-section">
  <div class="wi-container">
    <p class="wi-eyebrow">Alle Artikel</p>
    <h2 class="wi-h2" style="margin-top: 16px; margin-bottom: 0; max-width: 32ch;">
      Vollständige Veröffentlichungsliste.
    </h2>
  </div>
</section>
```

### F.2 — Query-Loop-Block einfügen

Wie E.2: `+` → „Query Loop" → „Start blank" → „Title, Date & Excerpt".

### F.3 — Query Loop konfigurieren — abweichend von E.3

- **Sortierreihenfolge**: Neueste zuerst
- **Elemente pro Seite**: `6`
- **Sticky-Beiträge**: **„Exclude sticky posts"** *(nicht „Only")*

### F.4 — Pagination behalten und anpassen

Diesmal NICHT entfernen. Stattdessen:

1. In der Listenansicht den **„Query Pagination"**-Block aufklappen
2. Er sollte drei Kinder haben: **„Pagination Previous"**, **„Pagination Numbers"**, **„Pagination Next"**
3. Falls einer fehlt, über `+` ergänzen
4. Bei Previous/Next die Texte anpassen: z.B. **„← Neuere"** und **„Ältere →"**

### F.5 — Inhalt gruppieren ⚠️ KRITISCH

Wie E.5: Post Title, Post Date, Post Excerpt im Post Template markieren, „Gruppieren".

### F.6 — CSS-Klasse setzen — abweichend von E.6

Im Feld „Zusätzliche CSS-Klasse(n)" eintragen:

```
wi-article-card
```

### F.7 — Post Terms ergänzen

Wie E.7.

### F.8 — Read More ergänzen

Wie E.8.

### F.9 — Post Title als Link

Wie E.9.

### F.10 — Layout: Grid wird automatisch durch CSS gesetzt

Sie müssen **nichts** im Editor auf Grid umstellen. Die CSS-Regel mit `:has(.wi-article-card)` aus Teil A.3 macht das automatisch — sobald das Post Template Karten mit dieser Klasse enthält, wird es als 3-Spalten-Raster gerendert.

### Checkpoint F

Speichern und Vorschau. Prüfen:
- ✓ Unterhalb des Featured Articles erscheint ein 3-Spalten-Raster
- ✓ Jede Karte hat weißen Hintergrund mit feinem Rahmen
- ✓ Beim Mouseover wechselt der Rahmen zu Teal
- ✓ Kategorien-Pill in helltürkis
- ✓ Pagination unter dem Grid

---

## Teil G — Newsletter-Signup (statisch)

Neuer Custom HTML Block:

```html
<section class="wi-section">
  <div class="wi-container">
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 64px; padding: 56px 64px; background: var(--wi-surface-soft); border-radius: 20px; align-items: center;">
      <div>
        <p class="wi-eyebrow" style="margin: 0 0 16px;">Newsletter</p>
        <h2 class="wi-h2" style="margin: 0 0 20px; font-size: clamp(26px, 3vw, 32px);">
          Alle neuen Artikel direkt im Postfach.
        </h2>
        <p style="font-size: 16px; line-height: 1.6; color: var(--wi-text-soft); margin: 0;">
          Maximal einmal pro Woche, oft seltener. Kein Tracking, kein
          Verkaufsdruck — nur die neuen Blog-Beiträge mit kurzer Einordnung,
          warum sie für werteorientierte Mittelständler relevant sein
          könnten. DSGVO-konform über mailbox.org.
        </p>
      </div>
      <div>
        <!-- Hier später Newsletter-Form einbinden (mailbox.org oder CentralStationCRM) -->
        <p style="font-size: 14px; color: var(--wi-text-muted); font-style: italic;">
          Newsletter-Formular wird hier eingebunden.
        </p>
      </div>
    </div>
  </div>
</section>
```

---

## Teil H — Final CTA (statisch)

Neuer Custom HTML Block am Ende der Seite:

```html
<section class="wi-section" id="kontakt">
  <div class="wi-container">
    <div class="wi-final-cta">
      <svg class="wi-final-cta-decor" viewBox="0 0 220 140" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <g fill="none" stroke="#FFFFFF" stroke-width="3.5" stroke-linecap="round">
          <path d="M 6 32 C 38 -2, 178 58, 214 36"/>
          <path d="M 6 68 C 38 32, 178 95, 214 72"/>
          <path d="M 6 104 C 38 68, 178 132, 214 108"/>
        </g>
      </svg>
      <p class="wi-eyebrow">Konkret werden</p>
      <h2 class="wi-h2">Aus einem Artikel zum konkreten Bedarf — in 30 Minuten klären wir, ob unsere Beratung zu Ihrer Situation passt.</h2>
      <div class="wi-final-cta-buttons">
        <a href="/kontakt#erstgespraech" class="wi-btn wi-btn-light">Erstgespräch buchen <span class="wi-arrow">→</span></a>
        <a href="/leistungen" class="wi-btn wi-btn-outline-light">Leistungen ansehen</a>
      </div>
    </div>
  </div>
</section>
```

---

## Teil I — Speichern und Live-Test

1. Oben rechts **„Aktualisieren"** klicken
2. Vorschau in neuem Tab öffnen
3. Checkliste komplett durchgehen:

| Sektion | Erwartete Anzeige | OK? |
|---------|-------------------|-----|
| Hero | Große Überschrift „Substanz statt Marketing" mit Lead-Text | ☐ |
| Themensäulen-Pills | „Alle Artikel"-Pill in Grün, 9 weitere in Weiß | ☐ |
| Featured Article Heading | „Aktueller Artikel" Eyebrow + H2 | ☐ |
| Featured Article Card | Sticky-Post mit Surface-Soft-Hintergrund, große Card | ☐ |
| Article Grid Heading | „Alle Artikel" Eyebrow + H2 | ☐ |
| Article Grid | 3-Spalten-Raster mit Karten | ☐ |
| Pagination | „← Neuere" / „Ältere →" unter dem Grid | ☐ |
| Newsletter-Sektion | Surface-Soft-Container, zweispaltig | ☐ |
| Final-CTA | Grüner Container mit weißen Wave-Linien | ☐ |
| Footer | Kadence-Footer mit waveImpact-Tagline | ☐ |

---

## Teil J — Troubleshooting

### Problem: Featured Article erscheint nicht

**Ursachen:**
1. Kein Sticky-Post angelegt → Beitrag öffnen → „Diesen Beitrag oben halten" aktivieren
2. Sticky-Posts-Filter steht auf „Include" statt „Only" → Query-Loop-Einstellungen prüfen
3. Items per page = 0 → auf 1 setzen

### Problem: Karten erscheinen als Liste, nicht als Grid

**Ursachen:**
1. Die `:has()`-CSS-Regel aus Teil A.3 ist nicht eingebunden → in Kadence Customizer prüfen
2. Der Group-Block hat nicht die Klasse `wi-article-card` → siehe F.6, oder DevTools-Inspektion auf das `class`-Attribut des Group-Elements
3. Browser-Cache → Strg+Shift+R (Hartes Neuladen)

### Problem: Karten haben WordPress-Default-Aussehen

**Ursachen:**
1. `waveImpact_queryloop_bridge.css` nicht in Kadence Custom CSS hinterlegt
2. CSS-Ladereihenfolge falsch (Bridge muss NACH global.css geladen werden)

### Problem: Kategorien werden nicht angezeigt

**Ursachen:**
1. Post Terms-Block ist auf Tags statt Kategorien gesetzt → Block-Einstellungen → Taxonomie auf „Kategorien"
2. Der Sticky-Post hat keine Kategorie zugewiesen → Beitrag öffnen → Kategorie zuweisen

### Problem: Group-Klasse wird nicht im DOM gerendert

**Ursachen:**
1. Die Klasse wurde im falschen Feld eingetragen → muss im Feld „Zusätzliche CSS-Klasse(n)" unter „Erweitert" sein, nicht im Klassen-Selector oben
2. WordPress hat das Speichern blockiert → Seite aktualisieren und erneut versuchen
3. Sicherheits-Plugin entfernt Custom Classes → temporär deaktivieren zum Test

### Problem: Post Title ist nicht klickbar

**Ursache:** Toggle „Titel zum Beitrag verlinken" nicht aktiviert → Post Title-Block selektieren → Block-Einstellungen → Toggle aktivieren

### Problem: Themensäulen-Links zeigen 404

**Ursache:** Category-Slugs in den Pill-Links stimmen nicht mit den tatsächlich angelegten Kategorien überein.

**Prüfung:** WP-Admin → Beiträge → Kategorien → Slug-Spalte gegen Pill-Links abgleichen.

---

## Teil K — Erweiterungen für später

### K.1 — Beitrags-Featured-Image im Featured-Block

Aktuell zeigt der Featured-Block kein Bild. Um das Featured Image zu integrieren:

1. In der Listenansicht den Group-Block `wi-featured-article` auswählen
2. Innerhalb des Groups einen **„Post Featured Image"**-Block einfügen (Position frei wählbar)
3. Die Bridge-CSS rendert das Bild automatisch im 4:3-Format

Voraussetzung: Jeder Beitrag braucht ein Featured Image (rechte Seitenleiste im Beitrags-Editor → „Beitragsbild").

### K.2 — Lesedauer anzeigen

Standard-WordPress berechnet keine Lesedauer. Optionen:

- **Plugin „Reading Time WP"** (kostenlos) → fügt automatisch Lesedauer hinzu
- **Manuell** über Custom Fields → pro Beitrag ein Feld `reading_time` pflegen, in Post Template als „Post Meta"-Block einbinden

### K.3 — Demnächst-Sektion (geplante Beiträge)

Beiträge mit Veröffentlichungsdatum in der Zukunft werden in WordPress als „Geplant" (Status `future`) gespeichert. Ein dritter Query Loop kann diese anzeigen:

- Einstellungen: Beitragstyp → Beiträge, Status-Filter „future"
- Eigene Klasse `wi-article-card wi-article-card--upcoming` (in der Bridge-CSS bereits vorbereitet — gestrichelter Rand + „Demnächst"-Badge)

Voraussetzung: Der Status-Filter benötigt das Plugin „Display Future Posts" oder einen Custom-Query-Filter — die native Gutenberg-UI bietet das nicht out-of-the-box.

### K.4 — Single-Post-Vorlage anpassen

Wenn Sie auf eine Karte klicken, lädt WordPress die Single-Post-Seite. Im Kadence-Theme können Sie die Single-Post-Vorlage über den **Kadence Theme Builder** (Pro-Funktion) im waveImpact-Look gestalten — Sidebar, Pull-Quote-Block, Verwandte-Artikel-Bereich am Ende.

### K.5 — Category-Archive-Vorlage

Wenn ein Besucher auf eine Themensäule-Pill klickt, lädt WordPress die Category-Archive-Seite. Standard ist die Theme-Default-Vorlage. Für Konsistenz sollten Sie diese Vorlage ebenfalls anpassen:

- Hero-Bereich mit dem Kategorienamen und der Beschreibung (aus A.1)
- Darunter ein Query Loop mit allen Beiträgen dieser Kategorie (wie F, aber `tax_query` filtert automatisch nach aktueller Kategorie)
- Pagination am Ende

Dafür entweder Kadence Theme Builder nutzen oder eine `category.php`-Vorlage im Child Theme anlegen.

---

## Abschluss

Wenn alle Checkpoints abgehakt sind, ist die News-Seite vollständig CMS-driven. Neue Posts erscheinen automatisch im Article Grid (sortiert nach Datum); ein als Sticky markierter Beitrag wandert automatisch in den Featured-Bereich; bestehende Featured-Posts wandern beim Entfernen des Sticky-Status zurück ins Grid.

Damit ist die statische Mockup-Phase abgeschlossen und die News-Sektion wird zum lebendigen Bestandteil Ihrer Veröffentlichungs-Infrastruktur.
