# waveImpact Startseite — Kadence-Integrationsleitfaden

**Stand:** Mai 2026
**Zielsystem:** WordPress mit Kadence Theme + Kadence Blocks (Free)
**Annahme:** Sie haben Admin-Zugriff und können das Theme sowie Plugins verwalten.

Dieser Leitfaden begleitet Sie Sektion für Sektion durch den Aufbau der neuen Startseite. Lesen Sie ihn einmal komplett, bevor Sie beginnen — die Reihenfolge der Vorbereitungsschritte (Schriften, Farben, Custom CSS) zahlt sich später aus.

---

## 1. Vorbereitung

### 1.1 Erforderliche Plugins

Stellen Sie sicher, dass folgende Plugins installiert und aktiv sind:

| Plugin | Zweck |
|---|---|
| **Kadence Blocks** (kostenlos) | Row Layout, Advanced Heading, Info Box, Advanced Buttons |
| **SVG Support** oder **Safe SVG** | Direkt-Upload von SVG-Logos und Hero-Visual |
| **WPForms Lite** (bereits aktiv) | Kontaktformulare, Lead-Magnet-Anfrage |

Optional, aber empfohlen:

- **Yoast SEO** oder **RankMath**: SEO-Meta für die neue Startseite.
- **WP Super Cache** oder **WP Rocket**: Page-Caching für Performance.

### 1.2 Schriften aktivieren

`Customize → Typography → Body Font:`
- **Family:** Lato
- **Variants:** Regular (400), Medium (500), Bold (700)
- **Subsets:** Latin, Latin Extended

`Customize → Typography → Heading Font:`
- **Family:** Lato (selbe Schrift, Hierarchie über Gewicht und Größe)
- **Default Weight:** 500

Optional für die Pull-Quote-Sektion:
`Customize → Typography → Custom Web Fonts:`
- **Family:** Lora — Variants Regular (400), Medium (500)
- Diese Schrift wird nur über die CSS-Klasse `.wi-pullquote-text` eingesetzt.

> **Hinweis:** Falls Sie keine zweite Webfont laden möchten, fällt die Pull-Quote automatisch auf `Georgia` zurück — das ist ebenfalls eine seriöse Antiqua und kein Qualitätsverlust.

### 1.3 Globale Farben anlegen

`Customize → Colors → Color Palette:`

Definieren Sie die Brand-Farben als Palette-Einträge, sodass Sie sie in jedem Block per Klick auswählen können:

| Slot | Hex | Verwendung |
|---|---|---|
| Color 1 (Primary) | `#059669` | Forest Green — Buttons, Akzente, CTA-Hintergrund |
| Color 2 (Secondary) | `#0D9488` | Ocean Teal — Eyebrows, sekundäre Akzente |
| Color 3 (Tertiary) | `#2DD4BF` | Helles Cyan-Teal — Logo-Wellen, Akzente |
| Color 4 (Text) | `#1F2937` | Dark Gray — Body-Text, Überschriften |
| Color 5 (Text-Soft) | `#4B5563` | Sekundärer Text |
| Color 6 (Surface) | `#F9FAFB` | Pull-Quote-Hintergrund, Sektions-Surface |

### 1.4 Custom CSS einbinden

`Customize → Additional CSS:`

Öffnen Sie die Datei `waveImpact_custom.css` aus dem Lieferpaket und kopieren Sie den gesamten Inhalt in das Additional-CSS-Feld. Speichern.

Falls Sie Kadence Pro nutzen: Verwenden Sie stattdessen `Kadence → Customizer → Global Custom CSS` — der Code wird dann theme-update-sicher gespeichert.

### 1.5 Assets hochladen

`Medien → Datei hinzufügen:`

Laden Sie folgende Dateien aus dem Lieferpaket hoch:

- `waveImpact_logo_mark.svg` — Drei-Wellen-Logo für Header
- `waveImpact_hero_visual.svg` — Hero-Komposition (Ripple + Wellen)
- `waveImpact_cta_decoration.svg` — Wellen für CTA-Hintergrund

> Falls SVG-Upload blockiert wird: Aktivieren Sie das SVG-Support-Plugin und stellen Sie sicher, dass Ihr User-Profil SVG-Berechtigung hat.

---

## 2. Aufbau Sektion für Sektion

### 2.1 Header

Im Kadence Header Customizer (`Customize → Header`):

- **Logo:** waveImpact_logo_mark.svg + Markenname als Text daneben
  - Falls Sie die Wortmarke separat möchten: Upload Logo-PNG mit Wortmarke
  - Logo-Höhe: 32 px (Desktop), 28 px (Mobile)
- **Navigation:** Leistungen, Expertise, News, Kontakt
- **Sprachumschalter:** Über Polylang-Block oder rechts vom Menü
- **Trennlinie unten:** 0.5 px solid rgba(0,0,0,0.10) — bereits im Custom CSS definiert

### 2.2 Hero-Sektion

**Block-Struktur:**

```
Row Layout (2 Spalten, 60/40)
├── Spalte 1 (links)
│   ├── Advanced Heading (P-Tag, Klasse: wi-eyebrow)
│   │   Text: "Responsible AI Consultancy · Bremen"
│   ├── Advanced Heading (H1, Klasse: wi-hero-headline)
│   │   Text: KI im Einklang<br/>mit Ihren <span class="wi-accent">Werten</span>.
│   ├── Paragraph (Klasse: wi-hero-subline)
│   │   Text: Dokumentiert, prüfbar, im Einklang mit dem EU AI Act — und mit dem, wofür Ihr Unternehmen steht.
│   └── Advanced Buttons (2 Buttons)
│       ├── Button 1 (Klasse: wi-btn-primary): "Kostenlose Risikoeinschätzung" → /eu-ai-act-risikoeinschaetzung/
│       └── Button 2 (Klasse: wi-btn-ghost): "Erstgespräch" → /kontakt/
└── Spalte 2 (rechts)
    └── Image-Block (oder Custom HTML)
        Bild: waveImpact_hero_visual.svg
        Max-Breite: 320 px
```

**Row-Einstellungen:**
- Layout: 2 Spalten, 60/40
- Vertikale Ausrichtung: Mittig
- Padding: Top 96 px, Bottom 80 px (Desktop) / Top 64 px, Bottom 56 px (Mobile)
- Spaltenabstand (Gap): 24 px

**Anchor-Setting des Hero-Bilds:**
Falls das SVG zu klein wirkt, im Image-Block die maximale Breite auf 280–320 px setzen und vertikal mittig ausrichten.

### 2.3 Stat-Strip

**Block-Struktur:**

```
Row Layout (3 gleiche Spalten, Klasse: wi-stat-strip)
├── Spalte 1
│   ├── Advanced Heading (Klasse: wi-big-num): "25+"
│   └── Paragraph (Klasse: wi-stat-label): "Jahre Digitalisierungserfahrung"
├── Spalte 2
│   ├── Advanced Heading (Klasse: wi-big-num): "8"
│   └── Paragraph (Klasse: wi-stat-label): "Module waveTest Prüfmethodik"
└── Spalte 3
    ├── Advanced Heading (Klasse: wi-big-num): "1"
    └── Paragraph (Klasse: wi-stat-label): "DBA Data Science, persönlich"
```

**Row-Einstellungen:**
- Padding: Top + Bottom je 32 px (wird über CSS-Klasse `.wi-stat-strip` gesetzt)
- Spaltenabstand: 24 px
- Vertikale Ausrichtung: Oben

> **Hinweis zur Zahl 8:** Diese steht für die acht Module der waveTest-Suite (Console, Fairness, Explain, DataQ, Comply, Monitor, Report, Sustain). Falls das Sustain-Modul aktuell noch in Spezifikation ist und nicht produktiv, setzen Sie hier eine 7 oder ersetzen Sie die Karte durch einen anderen Fakt.

### 2.4 Warum jetzt — Drei Value-Props

**Block-Struktur:**

```
Outer Row Layout (1 Spalte, Klasse: wi-section)
├── Advanced Heading (P-Tag, Klasse: wi-eyebrow): "Warum jetzt"
└── Inner Row Layout (3 gleiche Spalten)
    ├── Spalte 1
    │   ├── Advanced Heading (P-Tag, Klasse: wi-step-num): "01"
    │   ├── Advanced Heading (H3): "Die blinde Stelle"
    │   └── Paragraph: "KI entscheidet — der Nachhaltigkeitsbericht schweigt."
    ├── Spalte 2
    │   ├── Klasse: wi-step-num — "02"
    │   ├── H3: "Werte im Algorithmus"
    │   └── Paragraph: "Wir machen die Übersetzung sichtbar und prüfbar."
    └── Spalte 3
        ├── Klasse: wi-step-num — "03"
        ├── H3: "Governance unter Kontrolle"
        └── Paragraph: "Aus Werten wird Wettbewerbsvorteil — strukturiert."
```

**Spaltenabstand:** 24 px
**H3-Größe:** 15 px, Gewicht 500 (über Custom Class oder Block-Settings)

### 2.5 Pull-Quote

Dies ist die einzige Sektion, die ich Ihnen empfehle als **Custom HTML Block** umzusetzen — die absolute Positionierung des Logo-Markers lässt sich mit Standardblöcken nicht sauber abbilden:

```html
<div class="wi-pullquote">
  <img class="wi-pullquote-mark"
       src="/wp-content/uploads/2026/05/waveImpact_logo_mark.svg"
       alt="" />
  <p class="wi-pullquote-text">
    Wer KI einsetzt, übersetzt seine Werte in Code — ob bewusst oder nicht.
    Wir machen die Übersetzung sichtbar.
  </p>
  <p class="wi-pullquote-attribution">
    Dr. Valentin José Mayr · Gründer
  </p>
</div>
```

Pfad zum SVG ggf. anpassen — er hängt davon ab, wann Sie das Logo hochladen.

### 2.6 EU AI Act Timeline

**Block-Struktur:**

```
Outer Row Layout (Klasse: wi-section)
├── Inner Row Layout (2 Spalten, Verhältnis 70/30 für Header-Zeile)
│   ├── Spalte 1
│   │   ├── Advanced Heading (Klasse: wi-eyebrow): "EU AI Act"
│   │   └── Advanced Heading (H2, Klasse: wi-section-heading)
│   │       Text: Der Zeitplan hat sich verändert.<br/>Die Erwartungen nicht.
│   └── Spalte 2 (rechtsbündig, oben ausgerichtet)
│       └── Paragraph (klein, muted): "Stand: 7. Mai 2026"
└── Custom HTML Block (Timeline-Zeilen)
```

**Custom HTML für die Timeline-Zeilen:**

```html
<div class="wi-timeline-row">
  <span class="wi-pill wi-pill-neutral">Feb 2025</span>
  <p>Verbotene KI-Praktiken durchsetzbar</p>
</div>

<div class="wi-timeline-row">
  <span class="wi-pill wi-pill-warning">Aug 2026</span>
  <p>Transparenzpflichten (Art. 50) — <span class="wi-timeline-note">Frist bleibt</span></p>
</div>

<div class="wi-timeline-row">
  <span class="wi-pill wi-pill-info">Dez 2027</span>
  <p>Hochrisiko Anhang III — <span class="wi-timeline-note">verschoben aus Aug 2026</span></p>
</div>

<div class="wi-timeline-row">
  <span class="wi-pill wi-pill-info">Aug 2028</span>
  <p>Eingebettete Hochrisiko-KI Anhang I — <span class="wi-timeline-note">verschoben aus Aug 2027</span></p>
</div>

<p style="font-size: 13px; color: var(--wi-text-soft); margin-top: 1.5rem; max-width: 540px;">
  Mehr Zeit — gleiche Erwartungen. Investoren, Rating-Agenturen und Aufsichtsräte fragen heute schon.
</p>
```

### 2.7 Drei Wege, mit uns zu arbeiten

**Block-Struktur:**

```
Outer Row Layout (Klasse: wi-section)
├── Advanced Heading (P, Klasse: wi-eyebrow): "Zusammenarbeit"
├── Advanced Heading (H2, Klasse: wi-section-heading): "Drei Wege, mit uns zu arbeiten"
└── Inner Row Layout (3 gleiche Spalten, Spaltenabstand 12 px)
    ├── Spalte 1 — Custom HTML
    ├── Spalte 2 — Custom HTML (mit Featured-Klasse)
    └── Spalte 3 — Custom HTML
```

**Custom HTML pro Karte:**

Spalte 1 — Grundpaket:
```html
<div class="wi-service-card">
  <p class="wi-service-title">Grundpaket</p>
  <p class="wi-service-subtitle">Strategie und Standort</p>
  <p class="wi-price">18.000 €</p>
  <p class="wi-duration">ab · 4–6 Wochen</p>
</div>
```

Spalte 2 — Implementierung (mit Akzent):
```html
<div class="wi-service-card wi-service-card-featured">
  <span class="wi-badge-featured">Häufig gewählt</span>
  <p class="wi-service-title">Implementierung</p>
  <p class="wi-service-subtitle">Operationalisierung im Alltag</p>
  <p class="wi-price">35.000 €</p>
  <p class="wi-duration">ab · 3 Monate</p>
</div>
```

Spalte 3 — Transformation:
```html
<div class="wi-service-card">
  <p class="wi-service-title">Transformation</p>
  <p class="wi-service-subtitle">RAI als Differenzierung</p>
  <p class="wi-price">60.000 €</p>
  <p class="wi-duration">ab · 6+ Monate</p>
</div>
```

> **Entscheidung „Häufig gewählt":** Wenn Sie diese Aussage noch nicht durch Verkaufsdaten belegen können, ersetzen Sie das Badge-Wording durch „Empfohlen für etablierte Strukturen" oder lassen Sie das Badge komplett weg. Die grüne Umrandung allein hebt die Karte visuell genug ab.

### 2.8 Was uns unterscheidet

**Block-Struktur (verwendet Kadence Icon Block):**

```
Outer Row Layout (Klasse: wi-section)
├── Advanced Heading (Klasse: wi-eyebrow): "Was uns unterscheidet"
└── Inner Row Layout (3 gleiche Spalten, Spaltenabstand 24 px)
    ├── Spalte 1
    │   ├── Icon Block: microscope (Größe 28 px, Farbe #059669)
    │   ├── Advanced Heading (H3): "Forschung trifft Praxis"
    │   └── Paragraph: "DBA Data Science und 25+ Jahre operative Digitalisierung."
    ├── Spalte 2
    │   ├── Icon Block: tools
    │   ├── H3: "Eigene Prüfmethodik"
    │   └── Paragraph: "waveTest — reproduzierbar, statistisch belastbar, dokumentiert."
    └── Spalte 3
        ├── Icon Block: heart-handshake
        ├── H3: "Purpose vor Auslastung"
        └── Paragraph: "Selektiv, nicht skalierungsgetrieben. Partnerschaft statt Pipeline."
```

**Icon-Quelle:** Kadence Icon Block hat eine eingebaute Bibliothek. Suchen Sie nach „microscope", „tools" und „handshake" — wenn die exakten Tabler-Icons nicht verfügbar sind, nehmen Sie das nächste passende.

### 2.9 Schluss-CTA

**Block-Struktur:**

```
Row Layout (1 Spalte, Klasse: wi-final-cta)
├── Custom HTML (Dekorations-SVG)
│   <img class="wi-final-cta-decor"
│        src="/wp-content/uploads/.../waveImpact_cta_decoration.svg"
│        alt="" />
├── Advanced Heading (P, Klasse: wi-eyebrow): "Ihr nächster Schritt"
├── Advanced Heading (H2, Klasse: wi-final-cta-headline)
│   Text: "Wissen, wo Sie stehen — nicht als Pitch, sondern als Standortbestimmung."
└── Advanced Buttons (2 Buttons nebeneinander, Spaltenabstand 12 px)
    ├── Button 1 (Klasse: wi-btn-light): "30-Min.-Erstgespräch" → /kontakt/
    └── Button 2 (Klasse: wi-btn-outline-light): "5-Punkte-Schnell-Check (PDF)" → /downloads/schnellcheck/
```

**Row-Einstellungen:**
- Padding: Top + Bottom 56 px, Left + Right 40 px (Desktop)
- Hintergrundfarbe: nicht erforderlich, CSS-Klasse `.wi-final-cta` setzt sie
- Border-Radius: nicht erforderlich, CSS-Klasse setzt 16 px

### 2.10 Footer

Verwenden Sie den Kadence Footer Customizer (`Customize → Footer`):

- **Zeile 1:** Logo + Newsletter-Anmeldung (WPForms)
- **Zeile 2:**
  - Links: Impressum, Datenschutzerklärung
  - Rechts: Social-Links (LinkedIn, Bluesky, E-Mail)
- **Zeile 3 (Bottom-Bar):** Copyright + Firmenangaben
  - `© 2026 waveImpact GmbH · AG Bremen HRB 42134 HB`

---

## 3. SEO-Meta für die neue Startseite

In Yoast/RankMath (oder dem WordPress-eigenen SEO-Bereich):

**Title-Tag:**
`waveImpact — Verantwortungsvolle KI für werteorientierte Unternehmen`

**Meta-Description (max. 155 Zeichen):**
`KI-Governance, die zu Ihren Werten passt. Wir bringen Ihren KI-Einsatz in dokumentierte, prüfbare Übereinstimmung mit dem EU AI Act. Sitz Bremen, europaweit tätig.`

**OG-Image:** 1200×630 px, neues Hero-Visual auf weißem Grund mit Headline „KI im Einklang mit Ihren Werten."

> **Wichtig:** Die aktuelle Live-Seite trägt im OG-Description-Tag noch den alten Text „KI an einem Scheideweg …". Diesen müssen Sie hier neu setzen, sonst behält LinkedIn/Slack/E-Mail-Vorschauen den alten Wortlaut.

---

## 4. Test-Plan vor dem Live-Schalten

Bevor Sie die Seite öffentlich machen, prüfen Sie:

**Funktional**
- Alle Buttons führen zu existierenden Zielseiten (keine 404)
- Die Service-Karten-Links zeigen auf deutsche Unterseiten, nicht auf `/en/...`
- WPForms-Formulare senden zuverlässig (Mailbox.org-Routing, nicht Strato-SMTP)
- Sprachumschalter wechselt korrekt zwischen DE und EN

**Visuell**
- Hero-Visual rendert in Chrome, Firefox, Safari korrekt (SVG)
- Pull-Quote: Lora-Schrift lädt, kein Fallback-Flicker
- Mobil: Stat-Strip stapelt sauber untereinander
- Timeline-Pillen: Farben sind kontrastreich genug (mindestens 4.5:1 für WCAG AA)

**Technisch**
- Page Speed (Google Lighthouse Mobile): Ziel ≥ 90
- Total Blocking Time < 200 ms
- Cumulative Layout Shift < 0.1
- Largest Contentful Paint < 2.5 s

**SEO**
- robots.txt erlaubt Indexierung
- Sitemap.xml enthält die neue Startseite
- hreflang-Tags zwischen DE und EN gesetzt (über Polylang)
- Strukturierte Daten: Organization-Schema mit korrekter Adresse, LinkedIn-URL

---

## 5. Fehlerquellen und ihre Lösung

| Symptom | Wahrscheinliche Ursache | Lösung |
|---|---|---|
| Pull-Quote-Logo links überlappt Text | Mobile-Viewport | CSS-Media-Query in `waveImpact_custom.css` sorgt dafür — auf Update prüfen |
| Hero-Visual zu klein/groß | Image-Block-Max-Width nicht gesetzt | Im Image-Block max. 320 px setzen |
| Button-Hover wirkt blass | Theme-Default überschreibt Custom CSS | Im Custom CSS `!important` ist gesetzt — Cache leeren |
| SVG-Logo wird nicht angezeigt | SVG-Plugin nicht aktiv oder Berechtigung fehlt | Safe SVG-Plugin aktivieren, User-Rolle prüfen |
| Pillen-Farben wirken zu kontrastarm | Theme-Override | Im Custom CSS sind feste Werte gesetzt — Cache leeren, Browser-DevTools prüfen |
| Lora-Schrift lädt nicht | Kadence Custom Web Fonts nicht aktiviert | Customize → Typography → Custom Web Fonts → Lora hinzufügen |

---

## 6. Pflege nach dem Launch

- **Quartalsweise:** Timeline-Sektion prüfen — sobald der Digital-Omnibus formal angenommen ist (vor 2. August 2026 erwartet), den Hinweis „vorläufige Trilog-Einigung" entfernen.
- **Halbjährlich:** Preise und Paket-Beschreibungen abgleichen mit aktuellem Stand.
- **Anlassbezogen:** Stat-Strip aktualisieren, wenn Module zur waveTest-Suite dazukommen oder wegfallen.
- **Bei jedem Service-Update:** Die drei Service-Karten neu prüfen — wenn ein Paket umbenannt wird, im HTML-Block direkt ändern.

---

## 7. Liefer-Pakete-Übersicht

Dieser Leitfaden bezieht sich auf folgende Dateien aus dem Lieferpaket:

| Datei | Zweck | Wohin |
|---|---|---|
| `waveImpact_logo_mark.svg` | Drei-Wellen-Logo | Medienbibliothek, Header |
| `waveImpact_hero_visual.svg` | Hero-Ripple-Komposition | Medienbibliothek, Hero-Sektion |
| `waveImpact_cta_decoration.svg` | Wellen für Schluss-CTA | Medienbibliothek, CTA-Block |
| `waveImpact_custom.css` | Alle waveImpact-Styles | Customize → Additional CSS |
| `waveImpact_Kadence_Integration_Guide.md` | Dieser Leitfaden | Zum Nachlesen |

---

## 8. Wenn etwas hakt

Die häufigste Stolperfalle bei der Kadence-Integration ist die Reihenfolge der Custom-Klassen. Kadence rendert Klassen am Wrapper-Element des Blocks, nicht am inneren Element. Wenn ein Style nicht greift, prüfen Sie im Browser-DevTools, ob Ihre Klasse am erwarteten Element sitzt — gegebenenfalls verschachteln Sie ein zusätzliches Wrapper-Div via Custom HTML.

Falls Sie an einer Stelle nicht weiterkommen: Screenshot machen, dazu schreiben „erwartet vs. tatsächlich", und wir gehen die betreffende Sektion gemeinsam durch.

---

*Erstellt im Mai 2026 für waveImpact GmbH, Bremen. Dieser Leitfaden begleitet die Umstellung der Startseite auf die nach dem Digital Omnibus on AI vom 7. Mai 2026 aktualisierte Positionierung.*
