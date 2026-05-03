# BookaBox Cockpit · Redesign Brief

**Für:** Designer/Entwickler, der das BookaBox Cockpit von Grund auf neu baut
**Ausgangsbasis:** Bestehendes Cockpit auf cockpit.bookabox.com (Sprint 1+2 Stand)
**Zielplattform:** Mobile First (iPhone-Browser zu 80% — Jörn morgens beim Kaffee, Max im Auto/Büro), Desktop als zentrierte 520px-Spalte
**Sprache:** Deutsch primär, Englisch sekundär (i18n von Anfang an, Flag-Toggle 🇩🇪/🇬🇧, Default DE)
**Stack:** Single-File HTML mit Tailwind-ähnlichem Inline-CSS, Vanilla JS, kein React/Vue. Webhook-basierte Datenversorgung über n8n.

---

## 1. Warum ein Redesign

Das aktuelle Cockpit hat sich organisch über drei Sprints entwickelt und dabei das Kern-Versprechen verloren: **Sage mir in 5 Sekunden was heute wichtig ist.**

Drei konkrete Schmerzpunkte, die das Redesign auflösen muss:

**Schmerzpunkt 1 — "Heute" ist unsichtbar.**
Beim Öffnen des Cockpits sehe ich aktuell *Active Abos: 705*, *MRR: €77,4k*, *Belegung: 63,5%*. Das ist Status. Was ich aber wissen will: *Wie haben wir heute performed?* Wie viele Verträge sind heute reingekommen, wie viele m² hinzugewonnen, wie viel Mehrumsatz, wie sieht der Monats-Run gegen den Burn aus. Das fehlt komplett oder ist hinter Scrollen versteckt.

**Schmerzpunkt 2 — Burn vs. Profit über Portfolio ist nirgendwo.**
Es gibt eine OPEX-Tile mit "€297,8k vorläufig" und einen Hero mit "Margin April €14,9k". Aber die Beziehung zwischen beiden — *wo stehen wir heute im Monat? sind wir auf Kurs?* — ist nicht visualisiert. Kein Run-Rate-Vergleich, keine Tagesperformance gegen erwarteten Tagesschnitt.

**Schmerzpunkt 3 — Kein Pulse.**
Das aktuelle Cockpit ist statisch. Es gibt kein "Live-Gefühl", keine Veränderung erkennbar zwischen 9:00 und 18:00. Beim Refresh ändert sich nichts Sichtbares außer einer Live-Zeitanzeige. Für ein Operations-Cockpit das mehrmals pro Tag geöffnet wird, ist das tot.

---

## 2. Die Leitfrage des Cockpits

Jeder Pixel auf der Startseite muss diese Frage beantworten:

> **Heute, gerade jetzt — wie performed das BookaBox-Portfolio?**

Alles andere (Store-Detail-Drill-down, Mietanalytik, 12-Monats-Trend, Service-GmbH-Burn, VAT-Damage) ist sekundär und gehört in tiefere Ebenen. Die Startseite ist die **Tageszeitung**, nicht das Lexikon.

**Sub-Fragen die die Startseite mit beantwortet:**
1. Wie viele Verträge wurden heute geschrieben?
2. Wie viel m² wurden heute hinzugewonnen (oder verloren)?
3. Wie viel Mehrumsatz / MRR-Delta ist heute entstanden?
4. Sind wir auf Kurs zum Monatsziel oder läuft etwas aus dem Ruder?
5. Was ist akut auffällig (Lead unbeantwortet, Ticket alt, Standort unter Break-Even)?
6. Wie ist der Burn-vs-Profit-Stand des Portfolios — gerade jetzt?

---

## 3. Personas & Use Cases

### Max (CEO, 35, technikaffin)
- Öffnet das Cockpit 5-10× pro Tag
- Will *"Pulse"* — was hat sich seit dem letzten Blick geändert
- Geht oft tief in Store-Drill-down
- Nutzt iPhone (80%) und Desktop (20%, hauptsächlich abends für Plan-Vergleiche)

### Jörn (COO, 50+, weniger technikaffin)
- Öffnet das Cockpit 1-2× am Tag, meist morgens
- Will eine **Tageszeitung-artige** Zusammenfassung
- Nicht alle Standorte, nur Verantwortungsbereiche (Multi-Tenant, später)
- Nutzt fast ausschließlich iPhone, große Schrift wichtig

### Store-Manager (Multi-Tenant Stufe 2, später)
- Sieht nur seinen Standort
- Will operative Tageszahlen + offene Tickets/Leads

### Landlords (Multi-Tenant Stufe 3, später)
- Sieht nur seinen Standort, nur die für die Umsatzbeteiligung relevanten Werte
- Read-only, keine Drill-Downs

---

## 4. Information Architecture · Mobile First

Die Startseite ist eine vertikale Scroll-Erfahrung mit klar getrennten Schichten. Jede Schicht hat **eine Aufgabe**, nicht mehr. Reihenfolge ist normativ — nicht ändern ohne triftigen Grund.

### Schicht 1 — Topbar (sticky)

Höhe ca. 48px. Inhalt:
- Links: BookaBox-Wordmark · Schriftzug "Cockpit" daneben in kleiner Caps
- Mitte: 🇩🇪/🇬🇧 Sprach-Toggle, Theme-Toggle (Light/Dark)
- Rechts: Live-Indikator als grüner Dot + "Live · HH:MM"

Topbar bleibt beim Scroll oben kleben. Kein anderer Content.

### Schicht 2 — Tagespulse (Hero, kein Scroll nötig)

**Das ist die wichtigste Schicht.** Beim Öffnen sofort sichtbar, ohne zu scrollen.

```
HEUTE · 30. April 2026 · 14:23                [running]

+8 Verträge          +47 m²           +€892 MRR
heute reingekommen   neu vermietet    Mehrumsatz heute

     Burn-Run April · ████████░░░ 73% · noch 9 Tage
     OPEX 217k von 298k · Margin-Trend +€1,2k pro Tag
```

Konkret 4 Elemente:

**A) Datum-Stripe** — "HEUTE · 30. April 2026 · 14:23" + Status-Badge (running/closed)

**B) Drei große Tageszahlen** — nebeneinander, je 1/3 Breite. Auf Mobile bleiben sie nebeneinander auch bei 380px Viewport.
- Verträge heute (creations - churns) — grün wenn ≥0, rot wenn negativ
- m² heute — gleiche Logik
- MRR-Delta heute (Σ amount_signed) — gleiche Logik

Jede Zahl in 32-40px Silka Black, mit kurzer Beschreibung in 11px Caps darunter.

**C) Burn-Run-Balken** — eine horizontale Progress-Bar die zeigt:
- Wie weit sind wir im Monat (Tag X von Y) auf X-Achse
- Wo stehen wir mit OPEX gegen Plan-OPEX auf Y-Achse, oder einfacher: 
  - Linker Teil = bereits gebuchter OPEX
  - Voller Balken = erwartete OPEX-Summe Monatsende (aus Run-Rate hochgerechnet)
  - Markierung wo wir kalendarisch stehen (1./30.)
- Wenn OPEX-Run-Rate über Plan: roter Anteil, sonst grün/grau

Drei Lesarten in einer Visualisierung: Kalenderfortschritt, Geld-Fortschritt, On-Plan-vs-Off-Plan.

**D) Margin-Trend-Mini** — ein 11px-Subtext: *"Margin-Trend +€1,2k pro Tag · 9 Tage Restmonat"* mit Farbcode pos/neg.

### Schicht 3 — Auffälligkeiten (Quick View)

Direkt unter dem Hero. Zwei Kategorien:

**Akut · Heute** — nur was *heute* passiert ist und *jetzt* aktiv ist:
- Leads die heute reingekommen aber nicht beantwortet sind
- Tickets die heute eskalieren (SLA-Breach droht in <2h)
- Standorte die heute unter ihren Tagesschnitt rutschen

**Strukturell · Diese Woche** — was länger schwelt:
- Standort unter Break-Even seit X Tagen
- Lead älter als 14 Tage ohne Aktivität
- Customer mit überfälliger Zahlung > 30 Tage

Maximal 3-4 Karten. Wenn nichts akut ist: Leerstand mit grünem Häkchen "Heute alles im Plan."

### Schicht 4 — Standort-Pulse

Eine kompakte Liste der Standorte mit dem **Heute-Wert** prominent statt der MRR-Gesamtsumme.

Jede Zeile:
```
🇩🇪 Braunschweig    +3 / +18m²    €18,5k MRR · 87% BE
🇩🇪 Essen           +1 / +5m²     €12,5k MRR · ⚠ 92% BE
🇩🇪 Köln            0 / 0m²       €8,2k MRR · 🚨 unter BE
🇩🇪 Passau          +1 / +4m²     €5,5k MRR · 🚨 unter BE
🇪🇸 Palma           +3 / +20m²    €24,9k MRR · 78% BE
```

Sortierung: Nach BE-Status absteigend (kritischste oben), dann nach MRR.

Tap auf Zeile → Standort-Drill-Down (Sheet von unten).

### Schicht 5 — Portfolio-KPIs (kompakter Snapshot)

Erst hier kommen die Status-Werte die aktuell oben dominieren. Bewusst weiter unten, weil "Status" weniger dringlich ist als "Heute":

- Active Abos / Plan-Vergleich
- Belegung %
- MRR-Snapshot mit € pro m²
- Run-Rate Verträge/Monat (6mo Mittel)
- Year-End Forecast m²

Mehrspaltige Grid-Anzeige mit Tile-Cards. Auf Mobile 2 Spalten, ab 500px 3 Spalten.

### Schicht 6 — Tab-Bar (sticky bottom)

Fünf Tabs:
- **Heute** (default)
- **Stores** (alle Standorte mit Drill-Down)
- **Team** (Tickets, Leads, CRM-Pipeline)
- **Ask AI** (Claude-Sheet)
- **Refresh** (force reload)

Auf Desktop (≥640px): zentriert mit Max-Width 520px, gleicher Bottom-Anker.

---

## 5. Visuelle Sprache

### Typographie
- **Silka** (Primärfont) — Black für Headlines/KPI-Werte, SemiBold für Labels, Regular für Body
- Fallback in dieser Reihenfolge: `-apple-system, BlinkMacSystemFont, "Helvetica Neue", Arial, sans-serif`
- **JetBrains Mono** für Zahlenkolonnen in Tabellen und Mono-Akzente
- Skala (Mobile, +20% gegen aktuellem Cockpit für altersgerechte Lesbarkeit):
  - KPI-Big: 40px (Tagespulse), 26px (Portfolio-Tiles)
  - Headline: 24px Silka Black
  - Section-Title: 14px Silka SemiBold, Caps, Letter-Spacing 0.12em
  - Body: 16px Silka Regular
  - Caption / Sub: 11-12px Silka Medium, Color ink-3

### Farben (gemäß Brand-Skill: Grayscale + 1 Akzent)

**Light Mode:**
```
--bg-0:    #FFFFFF      Cards, primary surface
--bg-1:    #F6F5EF      Body background (off-white)
--bg-2:    #EEEDE7      Tile background
--ink-0:   #1A1A1A      Primary text
--ink-1:   #5F5E5A      Secondary text
--ink-2:   #888780      Tertiary
--ink-3:   #B4B2A9      Muted
--rule:    rgba(0,0,0,0.10)
--accent:  #BA7517      Amber — Akzentfarbe (sparsam, max 1 Element pro Sicht)
--pos:     #1D6B4F      Positiver Trend (Verträge +, m² +, MRR +)
--neg:     #A32D2D      Negativer Trend
--warn:    #854F0B      Warnung (auf BE-Schwelle, SLA-nah)
```

**Dark Mode:**
```
--bg-0:    #1F1F1D
--bg-1:    #161614
--bg-2:    #2A2A28
--ink-0:   #F0EFE9
--ink-1:   #B4B2A9
--ink-2:   #888780
--ink-3:   #5F5E5A
--rule:    rgba(255,255,255,0.10)
--accent:  #EF9F27      Amber heller für Dark Mode
--pos:     #5DCAA5
--neg:     #F09595
--warn:    #FAC775
```

**Akzent-Regel (Brand-konform):** Pro Sicht **genau ein** Element nutzt die Akzentfarbe. Auf der Startseite ist das die Burn-Run-Balken-Markierung "wo wir heute stehen". Alle anderen Highlights nutzen pos/neg/warn aus dem semantischen Set, nicht den Brand-Akzent.

### Spacing
- 4px Grid: 4 / 8 / 12 / 16 / 24 / 32 / 48
- Card-Padding: 16-20px
- Section-Spacing: 24-32px zwischen Schichten
- Tile-Gap: 8-12px

### Border-Radius
- Cards: 12-16px (groß, modern, nicht verspielt)
- Buttons / Chips: 8px
- Progress-Bars: 4-6px

### Schatten
Sparsam. Nur auf Sheets/Modals und auf der zentrierten Body-Container-Hülle (Desktop). Tiles brauchen keine Schatten — Border + Background-Differenz reicht.

---

## 6. Tonalität · Microcopy

### Sprache (gemäß Brand-Skill)

**Du-Ansprache, immer kapitalisiert.** *"Dein Portfolio", "Deine Standorte", "Du hast heute 8 neue Verträge geholt."*

**Kein Marketing-Sprech in einem Operations-Cockpit.** Cockpit ist intern, das ist die *informative Pole* nicht die *emotional/edgy*. Klar, präzise, knapp. Keine Floskeln wie "Großartig!", "Stark!", "Volltreffer!".

**Beispiele für Tagespulse-Microcopy:**

✅ Gut:
- *"+8 Verträge heute"*
- *"Heute alles im Plan."*
- *"Run-Rate auf Kurs · noch 9 Tage Restmonat"*
- *"3 Stores unter Break-Even — Palma am stärksten betroffen"*

❌ Vermeiden:
- *"Wow, 8 neue Verträge! 🎉"*
- *"Glückwunsch zum heutigen Erfolg"*
- *"Achtung: kritischer Standort!"*  (zu dramatisch)
- *"Beautiful day for BookaBox"* (Marketing-Sprech)

### Zahlenformatierung

**Deutsch (Default):** `1.234,56 €` — Punkt als Tausender-Trennzeichen, Komma als Dezimal
**Englisch:** `€1,234.56` — Komma als Tausender, Punkt als Dezimal

m²-Werte: immer 1 Nachkommastelle (`+47,3 m²`)
Verträge: ganze Zahlen mit Vorzeichen (`+8`, `-3`, `±0`)
Prozent: 1 Nachkommastelle (`87,3%`), außer wenn 0 oder 100 (dann ohne Komma)

Vorzeichen werden **explizit** gesetzt für Deltas: `+8`, `-3`. Bei `0` kein Vorzeichen.

### Datum/Zeit

**Deutsch:** `30. Apr. 2026 · 14:23`
**Englisch:** `Apr 30, 2026 · 2:23 PM`

Relative Zeiten erlaubt: *"vor 5 Min"*, *"heute morgen"*, *"gestern"*. Aber nur wo es Mehrwert hat — bei Statuswerten lieber absolute Zeit.

---

## 7. Interaktionen

### Refresh
- Pull-to-Refresh auf Mobile
- Refresh-Button in Tab-Bar (auf beiden Plattformen)
- Auto-Refresh alle 5 Minuten im Hintergrund
- Beim Refresh: dezent in der Topbar einen Spinner statt eines Full-Screen-Overlays

### Drill-Down
- Tap auf Standort-Zeile → Sheet von unten (75% Höhe)
- Tap auf Auffälligkeit → direkt zu Detail (Standort oder Team-Sheet)
- Im Sheet: Schwung-Geste nach unten zum Schließen, X-Button rechts oben

### Sprache wechseln
- Flag-Toggle in Topbar
- Sofortiger Re-Render ohne Reload
- Speichert Wahl in `localStorage` (außer wenn das in Artifacts blockiert ist — dann nur in Memory)

### Theme
- Folgt System-Default (`prefers-color-scheme`)
- Manueller Override über Topbar-Button
- Persistent in `localStorage` falls verfügbar

### Animationen
- Sehr zurückhaltend. 150-300ms, ease-out
- Beim Refresh: kurze Fade-In der neuen Werte (200ms)
- Keine Bouncing/Wobble/Cute-Animationen
- Tile-Tap: subtle Scale-Down auf 0.985 für 100ms (haptisches Feedback)

---

## 8. Datenverträge · Was das Backend liefern muss

**Wichtig für den Designer:** Diese Endpunkte existieren bereits. Das Redesign muss diese Schnittstellen respektieren oder ein Backend-Update mit-spezifizieren. Wenn Felder fehlen die das neue Design braucht, **explizit benennen** — nicht raten und Fallback-Logik im Frontend.

### Endpoint A: `GET /webhook/cockpit-core?token=…`
Liefert Portfolio-Snapshot + Stores. Workflow-ID `R2vxzcVdNy3Z1c1w`.

```json
{
  "generated_at": "2026-04-30T12:23:00Z",
  "period": "April 2026 (T30/30)",
  "period_short": "April 2026",
  "period_is_running": true,
  "period_day_of_month": 30,
  "period_days_in_month": 30,
  "date_today": "2026-04-30",
  "date_yesterday": "2026-04-29",
  "portfolio": {
    "mrr": 77400,
    "active": 705,
    "occupied_m2": 3395,
    "creations": 75,
    "churns": 54,
    "net_movement": 21,
    "locked": 56,
    "locked_rate": 7.9,
    "locked_risk": 5180,
    "today":     { "creations": 0, "churns": 0, "m2": 0, "mrr_signed": 0 },
    "yesterday": { "creations": 0, "churns": 0, "m2": 0, "mrr_signed": 0 },
    "last_7d":   { "creations": 0, "churns": 0, "m2": 0, "mrr_signed": 0 },
    "last_30d":  { "creations": 0, "churns": 0, "m2": 0, "mrr_signed": 0 },
    "monthly_series": [...]
  },
  "stores": [
    {
      "cid": 5, "name": "Braunschweig", "country": "DE",
      "mrr": 18567, "active": 210, "occupied_m2": 875.1,
      "eur_per_m2": 21.22,
      "today":     {...}, "yesterday": {...},
      "last_7d":   {...}, "last_30d":  {...},
      "monthly_series": [...]
    }
  ]
}
```

**Felder die das neue Design braucht und die ggf. nachgezogen werden müssen:**
- `portfolio.eur_per_m2` (aktuell nur per Store) — Frontend-Fallback `mrr/occupied_m2`
- `portfolio.today.mrr_today_eur` — heutiger MRR-Zuwachs in € (für Tagespulse-C)
- `today.events_count` pro Store (für Pulse-Liste)

### Endpoint B: `GET /webhook/cockpit-finance?token=…`
Liefert OPEX, Plan-Werte, 12mo-Trend. Workflow-ID `iNIzMSsEEQZyhlTN`.

```json
{
  "generated_at": "2026-04-30T12:23:00Z",
  "period": "April 2026",
  "stores": [
    {
      "cid": 5,
      "opex": 16700, "opex_clean": 16500,
      "opex_by_category": { "miete": 12600, "marketing": 800, ... },
      "miete": 12600, "umsatzbeteiligung": 0,
      "nebenkosten": 1100, "wasserschaden": 200,
      "gross_m2": 1800,
      "monthly_rent_target": 12600,
      "target_eur_per_m2": 7.00,
      "planned_gain_m2": 50,
      "rent_per_m2": 7.00,
      "nk_per_m2": 0.61,
      "nk_status": "ok",
      "m2_12mo_series": [...],
      "m2_12mo_avg": 73.8,
      "monthly_13mo": [...]
    }
  ],
  "nk_benchmark": 1.50
}
```

**Felder die das neue Design braucht:**
- `opex_run_rate_to_eom` — projezierter OPEX-Stand zum Monatsende (Tagesschnitt × verbleibende Tage + bisheriger Stand)
- `opex_today` — heute gebuchte Eingangsrechnungen
- `margin_run_rate_per_day` — Margin-Trend pro Tag im laufenden Monat

### Endpoint C: `GET /webhook/cockpit-occupancy?token=…`
Liefert net rentable m² aus `box.location` und ETA-Berechnungen.

### Endpoint D (Team): `GET /webhook/team-helpdesk` und `GET /webhook/team-crm`
Tickets und CRM-Leads für Auffälligkeiten-Sektion.

---

## 9. Berechnungs-Definitionen

Damit das Redesign nicht im selben Vagheits-Sumpf landet wie das aktuelle Cockpit:

### Tagespulse-Werte
- **Verträge heute** = `Σ portfolio.today.creations - Σ portfolio.today.churns` über alle aktiven Stores
- **m² heute** = `Σ portfolio.today.m2` (signed)
- **MRR-Delta heute** = `Σ portfolio.today.mrr_signed`

Quelle: `sale.order.log` mit `event_date = today` aus dem Core-Endpoint.

### Burn-Run-Balken
- **OPEX-Stand bisher** = `portfolio.opex_clean` (heute gebuchte Eingangsrechnungen, ohne Wasserschaden)
- **OPEX-Forecast Monatsende** = `opex_clean / day_of_month × days_in_month` (linear hochgerechnet)
- **OPEX-Plan** = `Σ store.monthly_rent_target` aus `bab.target` über Stores (oder leer wenn nicht gepflegt)
- **Position-Marker auf Balken** = `day_of_month / days_in_month × 100%`

Wenn `OPEX-Forecast > OPEX-Plan × 1.10`: roter Balken-Anteil, sonst grün.

### Run-Rate Verträge/Monat
6mo gleitender Mittelwert von `(creations - churns)` aus `monthly_13mo`. Aktuelle Formel im Cockpit, übernehmen.

### Year-End Forecast
`YTD_net + run_rate × remaining_months`. Aktuelle Formel im Cockpit, übernehmen.

### Break-Even pro Store
`opex_clean / eur_per_m2 = m²_at_BE` → Vergleich mit `occupied_m2` → Gap × `avg_monthly_net_m2` = Time-to-BE in Monaten.

### Margin-Trend pro Tag
`(mrr_to_date - opex_to_date) / day_of_month` — durchschnittlicher Tages-Margin-Beitrag im laufenden Monat.

### Akut-Schwellen für Auffälligkeiten

**Heute akut:**
- Lead seit > 4h heute eingegangen, nicht beantwortet → akut
- Ticket SLA-Deadline in < 2h → akut
- Standort hat heute `creations - churns < 0` UND keine andere Bewegung → akut

**Strukturell:**
- Lead älter als 14 Tage ohne Aktivität → strukturell
- Standort unter BE seit > 30 Tagen → strukturell
- Customer überfällig > 30 Tage mit > €100 → strukturell

---

## 10. i18n · Internationalisierung

**Architektur-Anforderung:** i18n von Anfang an, nicht nachträglich.

### String-Tabelle

Alle UI-Strings in einer zentralen Map am Anfang der Datei:

```javascript
const I18N = {
  de: {
    'today': 'Heute',
    'contracts_today': 'Verträge heute',
    'm2_today': 'neu vermietet',
    'mrr_today': 'Mehrumsatz heute',
    'all_on_track': 'Heute alles im Plan.',
    'days_remaining': 'Tage Restmonat',
    // ...
  },
  en: {
    'today': 'Today',
    'contracts_today': 'Contracts today',
    'm2_today': 'new m² rented',
    'mrr_today': 'extra revenue today',
    'all_on_track': 'Everything on track today.',
    'days_remaining': 'days left in month',
    // ...
  }
};

let LANG = 'de';
const t = (key) => I18N[LANG][key] || key;
```

### Lokalisierte Formatierung

```javascript
const fmtNumber = (n, opts = {}) => {
  const locale = LANG === 'de' ? 'de-DE' : 'en-US';
  return new Intl.NumberFormat(locale, opts).format(n);
};

const fmtEUR = (n) => fmtNumber(n, { style: 'currency', currency: 'EUR', maximumFractionDigits: 0 });
const fmtM2 = (n) => fmtNumber(n, { maximumFractionDigits: 1 }) + ' m²';
const fmtPct = (n) => fmtNumber(n, { maximumFractionDigits: 1 }) + '%';
```

### Sprachwechsel ohne Reload

Beim Klick auf Flag: `LANG` ändern, alle Sektionen re-rendern (`renderHero()`, `renderPulse()`, etc.), `localStorage.setItem('lang', LANG)` setzen.

---

## 11. Accessibility

- Alle interaktiven Elemente mit `role` und `aria-label`
- Tap-Targets mindestens 44×44px (Apple HIG)
- Kontrast WCAG AA: schwarz auf weiß ist easy, aber `--ink-3` Werte gegen `--bg-2` prüfen — kann dünn werden im Light Mode
- `prefers-reduced-motion` respektieren — Animationen aus
- Keyboard-Navigation für Desktop: Tab durch Tiles, Enter für Drill-Down

---

## 12. Performance-Budget

- **Initial Paint < 1s** auf 4G iPhone
- **Time to Interactive < 2s**
- HTML-Datei selbst < 100KB (das aktuelle Cockpit ist bei 190KB — definitiv zu groß)
- Keine externen Dependencies bei initial load (inkl. keine Fonts von Google)
- Chart-Library: nur lazy load wenn Charts gebraucht werden (Drill-Down-Sheets)

---

## 13. Was NICHT in das Redesign gehört (Sprint 4+)

Bewusst ausgeschlossen, damit das MVP fokussiert bleibt:

- ❌ Smart Metering (Verbrauchskosten Strom/Wasser pro Monat) — Sprint 4+
- ❌ VAT-Damage-Berechnung — kommt aus Odoo Server Action später
- ❌ Service-GmbH Burn / Overhead-Allocation — Sprint 4+
- ❌ AllroundTown NOI-Anteilig zugewiesen — Sprint 4+
- ❌ Multi-Tenant-Login (Magic-Link, Portal-Users) — separate Implementierung
- ❌ Pre-Launch-Pipeline für Hannover/Bochum — Sprint 4+
- ❌ Offline-Modus / PWA — kann später kommen wenn Need da ist

---

## 14. Akzeptanzkriterien

Das Redesign ist erst dann fertig wenn alle 12 Punkte erfüllt sind:

1. ☐ Beim Öffnen sehe ich ohne Scrollen: heute Verträge, heute m², heute MRR-Delta
2. ☐ Burn-Run-Balken zeigt mir wo wir im Monat stehen vs. wo OPEX gerade läuft
3. ☐ Margin-Trend pro Tag ist sichtbar
4. ☐ Auffälligkeiten-Sektion trennt akut (heute) von strukturell (länger schwelend)
5. ☐ Standort-Pulse zeigt Heute-Werte pro Standort, nicht nur Status
6. ☐ Tab-Bar zentriert auf Desktop ≥640px (kein Drift links — bekannter Bug)
7. ☐ Sprachwechsel DE↔EN ohne Reload
8. ☐ Alle Tap-Targets ≥44×44px
9. ☐ Pull-to-Refresh funktioniert auf Mobile
10. ☐ Initial Paint < 1s auf 4G
11. ☐ Dark Mode + Light Mode beide voll polished
12. ☐ Alle Strings durchgehend `t('key')` — keine Hardcoded-Texte ausser im Brand-Wordmark

---

## 15. Entwicklungs-Reihenfolge (empfohlen)

1. **Tag 1:** HTML-Skelett + CSS-Variablen + Topbar + Tab-Bar + Light/Dark Mode
2. **Tag 2:** Tagespulse (Schicht 2) — die wichtigste Schicht, mit Mock-Daten
3. **Tag 3:** Burn-Run-Balken — eigene Komponente, mathematisch sauber
4. **Tag 4:** Auffälligkeiten + Standort-Pulse mit echten Daten von n8n
5. **Tag 5:** Portfolio-KPIs + Drill-Down-Sheets
6. **Tag 6:** i18n-Integration + Sprachwechsel testen
7. **Tag 7:** Polish, Performance, Akzeptanzkriterien durchgehen

---

## 16. Brand-Guardrails (Kurz-Recap)

- ✅ Wordmark: **BookaBox.com** (camelCase mit `.com`)
- ✅ Du-Ansprache, kapitalisiert: **Dir, Dein, Dich**
- ✅ Claim: **"Mach' Dir Dein Leben einfacher"** — wenn überhaupt verwendet
- ✅ Silka als Primärfont
- ✅ Grayscale + 1 Akzent (Amber) — niemals zwei Akzentfarben in einer Sicht
- ✅ Fünf Werte: Einfachheit, Zuverlässig, Empathie, Gemeinschaft, Autonomie
- ❌ Niemals "Sie", "Wir", oder andere Anreden in DE
- ❌ Keine Marketing-Floskeln im operativen Cockpit
- ❌ Keine Fake-Stats / keine erfundenen Zahlen
- ❌ Kein generischer SaaS-Look (vermeide pastellige Farbpaletten, runde Cute-Icons, Confetti-Animationen)

---

## 17. Open Questions (vor Designstart klären)

1. **Burn-Definition pro Tag:** Linear über Monat verteilt (aktuell impliziert) oder Stichtags-genaue OPEX-Buchungen abbilden? Erstere Variante glättet, zweite ist ehrlicher aber zackiger.

2. **MRR-Delta heute:** Aus `sale.order.log.amount_signed` ist klar — aber: zählt eine Boxgrößen-Änderung als Mehrumsatz, oder nur Neuverträge? Definition fixieren.

3. **Sprache: Spanisch?** Palma-Standort hat ggf. spanische Stakeholder. Aktuell nur DE/EN geplant. Soll ES als drittes vorbereitet werden (i18n-Map mit `es` leer beginnen)?

4. **Multi-Tenant-Vorbereitung:** Soll das Redesign schon Layout-Slots für eingeschränkte Sichten haben (Store-Manager sieht nur 1 Store, Landlord sieht reduzierte KPIs)? Oder wird das ein Nachzug?

5. **Push-Notifications:** Soll der Tagespulse auch als Morning-Push aufs Handy gehen (z.B. um 7:30 mit den Vortageszahlen)? Das ist eine separate WhatsApp/Apple-Push-Pipeline, aber das Design sollte den Output-Schnitt antizipieren.

---

**Ende des Briefings.**

Bei Rückfragen oder Unklarheiten: lieber einmal mehr fragen als einen falschen Pfad einschlagen. Die wichtigste Regel ist die Leitfrage in Abschnitt 2 — alles muss diese Frage beantworten oder weichen.
