# BookaBox.com Brand Guide

> Authoritative source for BookaBox.com brand rules. Derived from the master brandbook (`230918_BaB-Brandbook.pdf`, Stand 18. September 2023, 66 pages, copyright BookaBox Service GmbH) by direct extraction. Cross-checked against the Vermieter-PDF (Stand Februar 2025) and the BookaBox.com Fund deck (April 2026).

This is the single document any BookaBox creative or marketing output is measured against. If something is not specified here, the rule has not been set yet — say so explicitly and propose an extension rather than inventing one.

## 1. Brand story (S. 3)

> Wir bieten Dir mehr als dreidimensionalen Raum. Mehr als Höhe, Länge und Breite.
>
> **Wir geben Dir die Einfachheit zurück.**
>
> Denn in einer sich immer schneller verändernden Welt braucht das Leben ab und an einfach einen Zwischenspeicher. Weil es manchmal unvorhersehbar ist, eigenartig, einzigartig, individuell. So bleibt Dir mehr Zeit für das was wirklich wichtig ist. Ganz einfach.
>
> Unsere flexible Self-Storage Plattform bietet mehr als Lagerfläche. Gestalte Deinen Raum ganz einfach so, wie Du ihn brauchst, ohne Ballast. Mit genau den Services, die Dir jetzt wichtig sind.
>
> Und wenn morgen ein neues Abenteuer für Dich wartet? Kein Problem: Wir haben den Raum, den Du dafür brauchst. Und vieles mehr.
>
> Genau dann, wenn Du es brauchst.
>
> **Mach' Dir Dein Leben einfacher.**

This is the canonical brand story. Reuse phrasings and rhythm from it freely in new copy.

## 2. Markenmodell (S. 4)

The five-layer model that underpins every brand decision.

### Purpose
> Wir schaffen Freiraum für Dich. Und bringen Dir die Einfachheit zurück. Mit einem Ort für das, was Dir wichtig ist.

### Vision
In einer komplexen, sich immer schneller verändernden Welt ist Einfachheit wertvoller als je zuvor. Wir glauben, schnell verfügbarer und flexibler Raum und individuelle Lösungen bedeuten auch mehr Zeit für das, was wichtig ist. Ganz einfach.

### Werte (the five values — fixed, do not rename)

| Wert | Aussage | Persönlichkeitsattribut |
|---|---|---|
| **Einfachheit** | Wir wollen Deinen Alltag jeden Tag etwas einfacher machen. | klar |
| **Zuverlässig** | Wir agieren transparent, zuverlässig, glaubwürdig, verbindlich. | authentisch |
| **Empathie** | Wir hören Dir aufmerksam zu und verstehen Dich. | einfühlsam |
| **Gemeinschaft** | Verbinde Dich mit Menschen und Lösungen. Wir bieten Dir die Plattform dafür. | verbindend |
| **Autonomie** | Gestalte die Dinge so, wie Du sie brauchst. Wir haben die Tools für Dich. | unterstützend |

### Versprechen / Claim
**"Mach' Dir Dein Leben einfacher."** — consumer default.
**"Mach' Dir Dein Leben leichter."** — formal / institutional / investor-facing variant (Fund deck precedent).

No other variants are sanctioned.

### Angebot
Wir bieten alles, was rund ums Lagern gebraucht wird — freier und sicherer Raum, plus eine digitale Self-Storage-Plattform mit Services, die der Kunde selbst gestalten kann. Ohne Ballast. Einfach, modular, flexibel. Analog und virtuell.

## 3. Address & language

- **Du, capitalized:** "Dir", "Dein", "Dich". Never "Sie" in consumer-facing German.
- **Primary language:** German.
- **English:** "you" lowercase per English convention. The official claim has no fixed English translation — keep the *spirit* of "make your life easier" but do not invent a new official line.

## 4. Wordmark and logo (S. 6)

The brandbook displays the logo in **four equal-status variants** on S. 6:

1. **Wordmark on light** — `BookaBox.com` in Silka Bold, black on white
2. **Wordmark on dark** — `BookaBox.com` in Silka Bold, white on black
3. **Pill on light** — `BookaBox.com` in Silka Bold inside a **black rounded-pill capsule**, used as CTA-button
4. **Pill on dark** — `BookaBox.com` in Silka Bold inside a **white rounded-pill capsule**, used as CTA-button on dark/colored surfaces

The pill variant is **not just a button style** — it's an officially sanctioned alternate logo form. It appears as a CTA button in every OOH and web mockup throughout the brandbook.

### Wordmark spelling
Always **"BookaBox.com"** in Silka Bold. CamelCase, with the ".com". The ".com" is part of the mark.

Wrong: BookaBox (missing .com), Bookabox (wrong casing), BOOKABOX (all-caps), BookABox (wrong internal casing)

### Social avatar — "BaB"
For social media profile avatars (Instagram, etc.), the wordmark abbreviates to **`BaB`** — lowercase `a` in the middle, since the abbreviation is **B**ook**a**Box. **Never `BoB`** with a lowercase `o`. Set in Silka Bold inside a circular black-on-white or white-on-black mark.

See `references/tokens.md` § Logo for implementation details and `references/brandbook-images/p06-logo.jpg` and `p25-detail-bab-avatar.jpg` for visual reference.

## 5. Typography — Silka (S. 7–8)

**Silka is the only brand typeface.** No Helvetica, no Arial, no Inter, no Montserrat — these are emergency-only fallbacks and must be flagged as such.

### Primary typestyles (S. 7) — top-level communication
- **Silka Bold** — the dominant headline weight. Hero claims, OOH headlines, presentation titles.
- **Silka Black** — heavier display variant for special emphasis. Use sparingly.
- **Silka Regular** — body copy default.

### Functional typestyles (S. 8) — when going deeper
- **Silka Medium** — sub-heads, structural labels
- **Silka Light** — long-form descriptions, secondary copy
- **Silka Regular Italic** / **Silka Light Italic** — quotes, captions, accents

### Reference text-style examples (from brandbook page templates)
- Topic / section title: 32pt Silka Bold
- Copy bold: 16pt / 20pt line-height
- Copy ultra light: 16pt / 20pt line-height
- Description regular: 14pt / 20pt line-height

These are reference proportions — the absolute size scales with the medium (poster vs. mobile vs. signage). Keep the relative hierarchy.

For implementation details (CSS `@font-face` declarations, fallback stack, weight numbers, file IDs of the font files in Drive), see `references/tokens.md` § Typography.

## 6. Color system (S. 9)

The brandbook S. 9 organizes color in three groups: Primary (white + black), Secondary (8-step grayscale ramp), Functional (4 hues — green, red, orange, blue). All hex codes have been eyedropped from the source page and are documented in `references/tokens.md` § Color.

### Quick summary of the canonical palette

**Primary** (S. 9):
- Brand White `#FFFFFF`
- Brand Black `#000000`

**Secondary — grayscale ramp** (S. 9): 8 steps from `#F5F5F5` to `#2B2B2B`

**Functional** (S. 9, 4 hues):
- Functional Green `#0D7A37` — success
- Functional Red `#D6454C` — error/alert
- Functional Orange `#FF9829` — warmth/energy (used in Fund deck)
- Functional Blue `#689ECC` — calm/info

**Highlight / campaign palette** (extended from OOH and social mockups, S. 13–17, 22, 25):
- ⭐ **Brand Coral Pink `#F25966`** — the dominant brand-warm highlight, used on the iconic OOH (S. 13) and Instagram mockup (S. 25). **Default highlight color for hero campaigns, presentations, social, OOH.**
- Brand Sand `#E0A868` — earthy
- Brand Bright Blue `#00A0E0` — cyan-bright, distinct from Functional Blue
- Brand Webbanner Green `#4CCE93` — for digital ads
- Plus Yellow, Teal, Soft Pink, Dusty Rose for variety

### Application rule (Hard Rule #7)
**Build in black and grayscale. Use one campaign color per piece, as a single highlight.** Typography, tables, charts, spreadsheets, and layout layers all live in the grayscale ramp. Campaign colors emphasize exactly one message per document/slide/page/chart — never two. If two things feel highlight-worthy, one of them isn't.

For most consumer-facing work, the default campaign color is **Brand Coral Pink `#F25966`**. The Fund deck (April 2026) uses **Functional Orange `#FF9829`** for institutional framing. Pick one — do not mix.

The interior color palette (RAL codes for physical wall, floor, and box surfaces at locations) is documented separately in `tokens.md` § Color — Interior / Architecture, drawing on brandbook S. 38.

## 7. Imagery (S. 10–11)

### People imagery (S. 10)
The brand uses a defined set of **8 canonical portrait motives** displayed in a 4×2 grid on brandbook S. 10. Each motive is photographed against a distinct campaign-color background (Coral Pink, Teal, Yellow, Hot Pink, Bright Blue, Dusty Rose, Sand, Soft Pink). See `references/imagery-index.md` for the catalog with persona mapping and `references/brandbook-images/p10-imagery-people.jpg` for the visual reference.

Note: Drive contains 11 Motiv files (`Motiv1.jpg` through `Motiv11.jpg`) — the discrepancy with the brandbook's 8 is unresolved (see `imagery-index.md` for details).

**Never use stock-photo people.** When a person is needed in BookaBox creative, use one of the 8 brandbook-canonical motives.

### Product imagery (S. 11)
The brandbook S. 11 displays 8 isometric renderings of storage box sizes (1m³, 1m², 2m², 3m², 5m², 8m², 10m², 15m²). These can be used in marketing materials to show what fits in each box size.

For real-world product imagery (boxes, kiosk, locations, app screens) the style is: clean, well-lit, real (not rendered), branded surfaces visible (wordmark or boxnumber).

## 8. Voice and tone (S. 13–25, 47)

See `references/voice-and-tone.md` for the full treatment. Short summary:

The brand voice operates on **two poles**:
- **Emotional / expressiv / edgy** — sharp, witty, observational. The brandbook's flagship campaigns are mostly recognition questions: *"Dein Schrank ist zu klein für zwei Persönlichkeiten?"*, *"Euer Einhorn wird zu groß für die Garage?"*, *"Werden Deine Akten langsam zum Akt?"*
- **Descriptive / informative** — calm, clear, functional. *"Smart. In 3 Klicks zur optimalen Lagerlösung."*

A given piece of work picks one pole and stays there.

There's also a third surface — **wall typography at locations** (S. 47) — with its own conventions: massive Silka Bold, single nouns/verbs ("Move", "Wo Dinge wohnen"), juxtaposed lists of artist names + furniture, first-person testimonials.

## 9. Locations

Currently in operation, opening, or planned (Stand Februar 2025, with updates from Fund deck April 2026):

| Standort | Adresse | Fläche | Status |
|---|---|---|---|
| BookaBox Braunschweig | Friederich Seele Straße 3, 38122 Braunschweig | 1.800 m² | In Betrieb |
| BookaBox Essen | Jägerstraße 26, 45127 Essen | 2.500 m² | In Betrieb |
| BookaBox Bochum | Castroper Hellweg 17–19, 44867 Bochum | 6.400 m² | Q1 2026 |
| BookaBox Hannover | Hildesheimer Straße 132, 33602 Bielefeld | 7.000 m² | Q4 2025 |
| BookaBox Bielefeld | Bahnhofstraße 15–17, 33602 Bielefeld | 4.600 m² | Q4 2025 |
| BookaBox Köln | Kurfürstenstraße 12, 50678 Köln | 500 m² | In Betrieb |
| BookaBox Passau I | Bahnhofstraße 28, 94032 Passau | 1.000 m² | April 2025 |
| BookaBox Passau II | Nikolastraße 2, 94032 Passau | 1.200 m² | Q4 2025 |
| BookaBox Palma de Mallorca | Calle 16 de Julio Nr. 56, 07009 Palma | 2.000 m² | Mai 2025 |

Status data may be outdated — check internal sources before publishing.

### Standort- und Gebäudeanforderungen (for landlord communication)
- Gebäudeart: Büro, Einzelhandel, Logistik
- Fläche: 500–10.000 m², bevorzugt 1.500–3.000 m²
- Lage: gut sichtbar, einfache Andienung; gemischte Entwicklung (mit Wohnungsbau / Einzelhandel) ist vorstellbar; reines Gewerbegebiet vermeiden
- Mietpreis: 4–7 €/m² je nach Lage, Qualität, Investitionsbedarf (Premium-Miete und Umsatzbeteiligung möglich)
- Investition: 150–200 €/m² einschließlich Box, Innenausstattung, Infrastruktur, Technik
- Sonstige Anforderungen: Erdgeschoss, Aufzug für andere Ebenen, Bodenvorbereitung nach BookaBox-Richtlinie (Industrieboden), Nutzungsänderung & Genehmigung falls erforderlich, Brandschutzanforderungen

Expansion contact: expansion@bookabox.com · +49 172 99 69 799

## 10. Product surfaces

The brand applies across these surfaces — see brandbook for full visual treatment:
- **Website** (Startseite, Product Detail, Location Overview)
- **Kundenportal**
- **Key App** (mobile)
- **Kiosk Screen** (at locations)
- **Out-of-Home Advertising** (poster, billboards) — Pole A territory, Coral Pink default
- **Webbanner** (Pole A, often Webbanner Green or Coral Pink)
- **Social Media** (account presence, post grids — `BaB` avatar)
- **Location signage** (outdoor signage, indoor signage, boxnumber, wall typography)
- **Standort Add-ons** (Paketsystem, Open Coworking)
- **Cargo trolley & toolwall** (interior infrastructure)
- **Pitch decks** (institutional, see `template-pitchdeck.md`)

## 11. Founders

- **Joern-Carlos Kuntze (JCK)** — Strategie, Company Builder, Finanz-Experte. Beteiligungen im Bereich Self-Storage und Gebäudedigitalisierung.
- **Maximilian Astroh** — Pionier auf dem deutschen Selfstorage-Markt, erfahrener Immobilienentwickler.

Use these names exactly as written when referenced in press, partner materials, or pitch decks.
