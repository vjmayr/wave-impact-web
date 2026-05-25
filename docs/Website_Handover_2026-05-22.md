# waveImpact Website — Handover-Dokument

**Erstellt:** 22. Mai 2026
**Letzte Session:** Website-Buildout, Kadence-Integration, CMS-driven News-Seite
**Status:** Website-Grundgerüst vollständig, Integration läuft, Veröffentlichung noch nicht erfolgt

---

## Teil 1 — Was wurde gemacht (Executive Summary)

Diese Session hat einen kompletten **statischen Website-Build** von 12 HTML-Seiten plus globale Design-System-CSS produziert, dann mit dem Kunden zusammen die **Kadence-Integration** durchlaufen. Die News-Seite ist als erste Seite vollständig CMS-driven implementiert; die anderen Seiten existieren als HTML-Vorlagen und warten auf Kadence-Integration.

**Tonalität & Brand-Positionierung:**
- "Purpose-First, nicht Compliance-First" — Werteorientierte B2B-Mittelständler im DACH-Raum
- Hanseatische Geradlinigkeit, Substanz statt Marketing
- Tonalität: Sie-Form, formell aber zugänglich
- Kein Lead-Magnet-Trichter, kein Tracking-Heavy-Setup

**Tech-Stack:**
- WordPress + Kadence Theme (Free-Version, kein Pro)
- mailbox.org für E-Mail (kein Strato-SMTP wegen Block)
- CentralStationCRM für Anfragen-Backend
- Simply Schedule Appointments (SSA) für Terminbuchung
- SimpleAnalytics (cookieless) für Analytics
- n8n als optionale Integration-Schicht

---

## Teil 2 — Vollständige Datei-Inventarliste

Alle Dateien liegen in `/mnt/user-data/outputs/` (während Claude-Sessions zugänglich).

### Brand-Assets
- `waveImpact_logo_mark.svg` — Drei-Wellen-Logo-Mark
- `waveImpact_logo_horizontal.svg` — Mark + Wordmark
- `waveImpact_hero_visual.svg` — Hero-Wellen-Komposition
- `waveImpact_cta_decoration.svg` — CTA-Block-Dekoration
- `waveImpact_AI_cleaned_nobg.png` — Logo-PNG (Projekt-Knowledge)

### Stylesheets
- `waveImpact_global.css` — 22 Sektionen, vollständiges Design-System
- `waveImpact_spacing_overrides.css` — v1.2 mit `:has()`-Selektoren (in Kadence aktiv)
- `waveImpact_queryloop_bridge.css` — Bridge zwischen WP-Query-Loop und Karten-Design (in Kadence aktiv)

### Seiten (statisches HTML)
1. `waveImpact_homepage_reference.html` — Homepage (Referenz)
2. `waveImpact_leistungen.html` — Leistungs-Übersicht
3. `waveImpact_leistungen_readiness.html` — S1 EU AI Act Readiness Assessment
4. `waveImpact_leistungen_audit.html` — S2 AI Ethics Audit & Bias Testing
5. `waveImpact_leistungen_monitoring.html` — S3 Continuous Monitoring
6. `waveImpact_leistungen_workshops.html` — S4 Responsible AI Workshops
7. `waveImpact_expertise.html` — Methodische Tiefe + waveTest
8. `waveImpact_ueber.html` — Über waveImpact + Werte + Gründer
9. `waveImpact_news.html` — News-Index (statische Referenz, Kadence-Version ist CMS-driven)
10. `waveImpact_kontakt.html` — Kontakt mit SSA-Shortcode + CSCRM-Embed
11. `waveImpact_impressum.html` — Impressum (vorläufige Fassung)
12. `waveImpact_datenschutz.html` — Datenschutzerklärung (vorläufige Fassung)
13. `waveImpact_styleguide.html` — Kitchen-Sink-Verifikationsseite

### Dokumentation
- `waveImpact_News_Seite_Setup_Guide.md` — Komplette Setup-Anleitung News-Seite (11 Teile)
- `waveImpact_Website_Handover_2026-05-22.md` — Dieses Dokument

---

## Teil 3 — Status pro Seite

| # | Seite | HTML | Kadence-Integration | Live |
|---|-------|------|---------------------|------|
| 1 | News (CMS-driven) | ✓ | ✓ vollständig | ⏳ |
| 2 | Kontakt | ✓ (mit SSA + CSCRM) | ⏳ ausstehend | ⏳ |
| 3 | Leistungen (Übersicht) | ✓ | ⏳ ausstehend | ⏳ |
| 4 | S1 Readiness | ✓ | ⏳ ausstehend | ⏳ |
| 5 | S2 Audit | ✓ | ⏳ ausstehend | ⏳ |
| 6 | S3 Monitoring | ✓ | ⏳ ausstehend | ⏳ |
| 7 | S4 Workshops | ✓ | ⏳ ausstehend | ⏳ |
| 8 | Expertise | ✓ | ⏳ ausstehend | ⏳ |
| 9 | Über | ✓ | ⏳ ausstehend | ⏳ |
| 10 | Homepage | ✓ (Referenz) | ⏳ ausstehend | ⏳ |
| 11 | Impressum | ✓ (vorläufig) | ⏳ ausstehend + ⚠️ Anwalt | ⏳ |
| 12 | Datenschutzerklärung | ✓ (vorläufig) | ⏳ ausstehend + ⚠️ Anwalt + Calendly→SSA-Update | ⏳ |

**Bonus — auf der Live-WordPress-Seite bereits:**
- ✓ 9 Kategorien angelegt (Themensäulen mit Slugs und Beschreibungen)
- ✓ Custom CSS in Kadence Customizer eingespielt (global + spacing overrides + queryloop bridge + sidebar-removal-Hack)
- ✓ News-Seite mit zwei Query Loops konfiguriert (Featured + Article-Grid)

---

## Teil 4 — Kritische offene Punkte (in dieser Reihenfolge angehen)

### 4.1 — VOR ALLEM ANDEREN: Datenschutzerklärung muss aktualisiert werden

⚠️ **WICHTIG:** Die aktuelle Datenschutzerklärung in `waveImpact_datenschutz.html` nennt in §9 **Calendly** als Terminbuchungs-Tool und beschreibt Drittland-Übermittlung in die USA. Diese Information ist **veraltet** — wir haben in der Kontakt-Seite Calendly durch **Simply Schedule Appointments (SSA)** ersetzt, das lokal in WordPress läuft und keine Drittland-Übermittlung verursacht.

**Konkret zu tun:**
1. §9 der Datenschutzerklärung umschreiben: SSA statt Calendly
2. §13 (Datenübermittlung in Drittländer) entsprechend anpassen — möglicherweise sogar streichen, da SSA keine Drittland-Übermittlung verursacht
3. SSA Plugin in §9 als "Selbst-Hosted, läuft auf demselben Server wie WordPress" charakterisieren

### 4.2 — Steuerliche Pflichten (laut User-Memory aus Mai 2026)

Aktuell zwei überfällige Umsatzsteuer-Voranmeldungen (Q4 2025, Q1 2026) mit Frist ca. 07.05.2026, Steuernr. 60/134/03404. Empfehlung: Notfall-Übergabe an Steuerberater Kessler/Osterloh für diese zwei Filings, Haftungsrisiko nach § 69 AO. **Dieser Punkt liegt strikt außerhalb des Website-Builds, sollte aber wegen Dringlichkeit zuerst erwähnt sein.**

### 4.3 — Rechtliche Pflichtangaben füllen

In Impressum und Datenschutzerklärung sind sechs Platzhalter zu füllen:

1. `[Straße + Hausnummer]` — tatsächliche Geschäftsadresse (Impressum §1, §6; Datenschutz §1)
2. `[+49 …]` — Telefonnummer (Impressum §3) — falls keine, ganze Zeile entfernen, da §5 TMG eine schnelle elektronische Kontaktmöglichkeit verlangt, was E-Mail allein erfüllt
3. `DE [USt-IdNr. einsetzen]` — Umsatzsteuer-ID (Impressum §5)
4. `[Versicherer einsetzen]` — Berufshaftpflicht-Versicherungsgesellschaft (Impressum §7)
5. **E-Mail-Adresse `datenschutz@waveimpact.de`** — separates Postfach in mailbox.org einrichten
6. **CSCRM-AVV** — muss tatsächlich abgeschlossen sein (Auftragsverarbeitungsvertrag mit 42he GmbH)

### 4.4 — Anwaltliche Prüfung Impressum + DSE

Beide Legal-Seiten sind als rechtssichere Strukturvorlagen erstellt, aber **vor Veröffentlichung muss ein IT-Recht-Anwalt sie prüfen**. In Deutschland sind Impressum und Datenschutzerklärung das mit Abstand größte Abmahn-Risiko für junge GmbHs. Bremen hat mehrere IT-Recht-Kanzleien (z.B. Brinkert Häckler, IT-Recht-Kanzlei.de). Empfehlung: 200-500 € Investition spart im Worst Case fünfstellige Abmahnkosten.

### 4.5 — Restliche Seiten in Kadence integrieren

Die anderen 11 Seiten müssen nach demselben Muster wie die News-Seite in Kadence übertragen werden. Da diese (anders als News) komplett statisch sind, ist es einfacher: Custom HTML Blocks mit dem bestehenden HTML einfügen.

**Vorgehen pro Seite:**
1. Neue WordPress-Seite anlegen
2. Sidebar via gleicher CSS deaktivieren (`.page-id-X .sidebar { display: none; }`)
3. Custom HTML Block(s) mit dem bestehenden HTML einfügen
4. Speichern und prüfen

**Alternative:** Globale Sidebar-Deaktivierung im Customizer setzen → einmal global statt pro Seite (siehe Punkt 4.7).

---

## Teil 5 — Funktionale Backlog-Punkte

### 5.1 — Backend-Integration

| Punkt | Status | Priorität |
|-------|--------|-----------|
| SSA Plugin: Event-Type "unverbindliche-beratung" konfigurieren | ⏳ ausstehend | hoch |
| SSA: Verfügbarkeitszeiten festlegen (Mo-Fr 9-18 Uhr) | ⏳ ausstehend | hoch |
| SSA: E-Mail-Bestätigungs-Template | ⏳ ausstehend | hoch |
| SSA: mailbox.org als Calendar-Sync | ⏳ ausstehend | hoch |
| CentralStationCRM-Form-Styling prüfen (ggf. CSS-Override) | ⏳ ausstehend | mittel |
| mailbox.org SMTP-Konfiguration (über Plugin wie WP Mail SMTP) | ⏳ ausstehend | mittel |
| Newsletter-Backend (mailbox.org oder über CSCRM) | ⏳ ausstehend | niedrig |
| n8n-Workflow für Form → CRM (optional) | nicht begonnen | niedrig |

### 5.2 — Sidebar-Lösung global statt per CSS-Hack

Der aktuelle Sidebar-Removal-Hack via `.page-id-X .sidebar { display: none; }` funktioniert, ist aber pro Seite zu pflegen. **Sauberer:** Im Kadence Customizer global „Disable Sidebar for Pages" setzen, dann müssen wir es nur einmal machen statt pro Seite.

**Aktion:** Customizer → General → Layout → Page Layout → Sidebar auf "Disabled" stellen.

### 5.3 — Content / Editorial

| Punkt | Status |
|-------|--------|
| Gründerfoto (Platzhalter "Foto folgt" auf Expertise- und Über-Seite) | ⏳ |
| LinkedIn-URL aktualisieren (`linkedin.com/in/valentinmayr`) | ⏳ |
| og:image-SVGs für Blog-Artikel | ⏳ |
| Featured Images für bestehende Anker-Artikel | ⏳ |
| Excerpts manuell pflegen für alle Beiträge (30-60 Wörter) | ⏳ |
| Anker-Artikel 1-6 als WordPress-Posts anlegen (aus bestehenden .docx) | ⏳ |
| Anker-Artikel ab Anker 7 (KI & Umwelt Serie Fortsetzung) produzieren | ⏳ |

### 5.4 — Single-Post & Category-Archive Templates

Wenn ein User auf einen Blog-Artikel oder eine Themensäulen-Pill klickt, lädt WordPress die Single-Post- bzw. Category-Archive-Seite. Aktuell sieht das aus wie der **Kadence-Default**, nicht wie der waveImpact-Look.

**Lösungswege:**
- **Kadence Theme Pro** (Lizenz nötig) → Theme Builder für einfaches visuelles Design
- **Child Theme** mit `single.php` und `category.php` (PHP-Aufwand)
- **CSS-Overrides** auf den Default-Templates (kompromissreich)

**Empfehlung:** Erst Kadence Pro-Lizenz bewerten (ca. 129 €/Jahr für ein Projekt), bevor PHP-Aufwand betrieben wird.

### 5.5 — Browser- und Mobile-Tests

Die Renderings in unseren Sessions wurden mit Playwright in Desktop-Viewport 1400×900 erzeugt. Echte Mobile- und Tablet-Tests stehen aus.

**Test-Matrix:**
- iPhone (Safari, neuestes iOS)
- Android (Chrome)
- iPad (Safari)
- Desktop Chrome
- Desktop Safari
- Desktop Firefox
- Desktop Edge

Besondere Achtung: SVG-Logos, FAQ-`<details>`-Verhalten, Query-Loop-Grid-zu-Stack-Umbruch, Hero-Headline-Größe auf Mobile.

### 5.6 — SEO

| Punkt | Status |
|-------|--------|
| sitemap.xml generieren (Plugin: Yoast oder Rank Math) | ⏳ |
| Robots.txt prüfen | ⏳ |
| JSON-LD Strukturierte Daten (Organization, Person, Service) | ⏳ |
| Meta-Descriptions systematisch (bereits in HTML, prüfen in WP) | ⏳ |
| og:image pro Seite | ⏳ |
| Sprach-Markup `<html lang="de">` (in den Templates korrekt) | ✓ |

### 5.7 — Performance & Accessibility

| Punkt | Status |
|-------|--------|
| Pagespeed Insights / Core Web Vitals messen | ⏳ |
| Lighthouse Audit | ⏳ |
| A11y-Audit (axe oder WAVE) | ⏳ |
| Image-Optimierung (WebP für Featured Images) | ⏳ |
| Font-Loading optimieren (font-display: swap?) | ⏳ |

### 5.8 — waveTest Sustain Modul (separater Workstream)

- v0.1 Spec vollständig (laut Memory)
- Dr. Zielke flagged für Methodology Review vor v1.0
- Im Whitepaper als "in Entwicklung" markiert
- Kein Website-spezifischer Punkt, aber Cross-Reference relevant für Expertise-Seite

---

## Teil 6 — Bekannte Probleme & Workarounds

### 6.1 — Kadence Free Sidebar-Layout

**Problem:** Kadence Free zeigt auf Seiten standardmäßig eine Sidebar mit Recent-Posts-Widget. Die Per-Page-Layout-Optionen sind beschränkt.

**Workaround:** CSS-Override pro Seiten-ID (`.page-id-X .sidebar { display: none !important; }` plus Grid-zu-Block-Hack für den Content-Container).

**Sauberere Langzeit-Lösung:** Global im Customizer Sidebar für alle Pages deaktivieren (siehe 5.2), oder auf Kadence Pro upgraden.

### 6.2 — Query Loop Layout-Setting nicht erreichbar in UI

**Problem:** Die Layout-Toggle-Option (Grid vs. List) für Query-Loop-Post-Templates ist in der aktuellen Kadence-Free-Konfiguration nicht in der UI erreichbar.

**Workaround:** CSS-Forcierung via `:has(.wi-article-card)`-Selektor in der Bridge-CSS. Funktioniert browser-seitig.

### 6.3 — Inline-Styles in HTML vs. Kadence-Block-Editor

**Problem:** Die HTML-Vorlagen verwenden viele `style="padding-block: ..."`-Inline-Styles. Beim Kadence-Block-Import können diese gestrippt werden.

**Workaround:** Spacing-Overrides v1.2 nutzt `:has()`-Selektoren, die Inhalts-basiert greifen, nicht Inline-Style-basiert.

**Langzeit-Refactoring:** Inline-Styles durch Modifier-Klassen ersetzen (`wi-section--hero`, `wi-section--standard`, etc.).

### 6.4 — Footer-Trennung

Die Custom-HTML-Blöcke enden mit `</section>`. Kadence rendert dann seinen eigenen Footer. Falls der waveImpact-Footer aus dem HTML-Template verwendet werden soll, muss er separat als globaler Kadence-Footer konfiguriert werden (Customizer → Footer Layout).

---

## Teil 7 — Strategische Punkte (außerhalb des Website-Builds)

### 7.1 — IHK Bremen Seminar

Konzept liegt vor (laut Memory): 2-teilige Serie "KI-Governance kompakt" mit Modul 1 (3.5h) und Modul 2 (7h). Pitch an IHK Bremen ausstehend.

### 7.2 — Joint AI Sustainability Report mit Dr. Zielke

Active priority (laut Memory). Inhaltliche Zusammenarbeit, Veröffentlichungsformat zu klären.

### 7.3 — Webinar-Replanning

Webinar zu KI-Governance im Nachhaltigkeitsbericht (war für 24.04.2026 geplant) wurde wegen geringer Registrierungen postponed. Retrospektive abgeschlossen. Re-Planning mit besserem Format, Targeting und ggf. Dr. Zielke als Co-Host ausstehend.

### 7.4 — LinkedIn Cascade Posts

Anker 7 (AI Monitoring) braucht LinkedIn-Cascade-Posts als KW-Paket, sobald Publikationsdatum feststeht.

### 7.5 — Steuerberater-Handover (Kessler/Osterloh)

Volle Übergabe noch nicht erfolgt. Notfall-Übergabe für die zwei überfälligen UStVA-Filings dringend (siehe 4.2).

---

## Teil 8 — Empfohlene Reihenfolge für den nächsten Chat

**Ich empfehle, die nächste Session in dieser Reihenfolge anzugehen:**

1. **Datenschutzerklärung aktualisieren** — Calendly raus, SSA rein (15 Min)
2. **Platzhalter füllen** in Impressum + DSE (manuell außerhalb des Chats, 30 Min)
3. **Globale Sidebar-Deaktivierung** in Kadence Customizer einstellen (5 Min)
4. **Restliche statische Seiten in Kadence integrieren** — als Custom HTML Blocks (4-6 Seiten pro Stunde, je nach Komplexität)
5. **Anwaltliche Prüfung** der finalen Impressum + DSE einleiten (außerhalb Chat)
6. **SSA Plugin konfigurieren** mit Event-Type, Verfügbarkeiten, E-Mail-Templates (1 Std)
7. **CSCRM-Form testen** und ggf. Styling-Override schreiben (30 Min Diagnose + 30 Min CSS, falls nötig)
8. **Erste Blog-Posts anlegen** — Anker 1-6 als WordPress-Posts mit Excerpt, Kategorie, ggf. Featured Image (1-2 Std)
9. **Single-Post & Category-Archive Templates** — Entscheidung: Kadence Pro oder Child Theme (separate Diskussion)
10. **SEO-Basics** — sitemap, JSON-LD, og:images (1-2 Std)

Die Punkte 1-4 zusammen sind ein gut machbares Chat-Paket. Punkte 5-10 sind dann separate Sessions oder eigene Workstreams.

---

## Teil 9 — Wichtige Kontext-Informationen für den nächsten Chat

**Wenn Sie einen neuen Chat starten, geben Sie diesem zur Übergabe:**

1. **Diese Handover-Datei** (`waveImpact_Website_Handover_2026-05-22.md`) — als Anhang
2. **Den Setup-Guide** (`waveImpact_News_Seite_Setup_Guide.md`) — als Referenz für News-Seite-Wartung
3. **Alle drei CSS-Dateien** — `waveImpact_global.css`, `waveImpact_spacing_overrides.css`, `waveImpact_queryloop_bridge.css`
4. **Die finalen HTML-Vorlagen** — alle 12 Seiten

Der nächste Claude-Agent kann auf dieser Basis nahtlos weitermachen, ohne dass Sie alles wieder erklären müssen. Erwähnen Sie kurz, welche der Punkte 1-10 aus Teil 8 Sie als nächstes angehen wollen, und der Agent kann direkt einsteigen.

**Memory-Stand prüfen:** In den User-Memories sollten die wichtigsten Eckpunkte aus dieser Session (Tools, Brand, Workflows) bereits hinterlegt sein. Falls ein neuer Chat etwas nicht zu kennen scheint, das hier dokumentiert ist, einfach diese Datei als Kontext einfügen.

---

## Teil 10 — Erkenntnisse aus dieser Session

Drei methodische Lernpunkte, die für künftige Arbeit hilfreich sein können:

**1. Mockup → CMS ist mehr Arbeit als gedacht.** Statisches HTML in Kadence/Gutenberg zu übersetzen bedeutet nicht „Copy-Paste". Inline-Styles werden gestrippt, Block-Hierarchien sind tief verschachtelt, und Layout-Settings sind in der UI manchmal nicht erreichbar. Lösung: robuste CSS-Bridge-Layer mit `:has()`-Selektoren, die Inhalts-basiert statt Struktur-basiert greifen.

**2. Kadence Free ist überraschend limitiert.** Wesentliche Per-Page-Konfigurationen (Sidebar, Layout, Templates) sind nur in der Pro-Version sauber zugänglich. Für ein professionelles Auftritts-Setup ist die Pro-Lizenz wahrscheinlich die kosteneffizienteste Investition.

**3. Substanz-CSS funktioniert über die ganze Strecke.** Das ursprüngliche Design-System (Lato + Lora, Forest Green, Surface Soft) hat sich beim Wechsel von statischen Mockups zur dynamischen WP-Integration als robust erwiesen. Keine Re-Designs nötig, nur Bridge-CSS-Erweiterungen.

---

**Ende des Handover-Dokuments.**
**Bei Fragen zur Interpretation einzelner Punkte: kurz im nächsten Chat angeben, welcher Punkt unklar ist.**
