# Design Tokens

> Authoritative implementation specs for BookaBox.com — colors, typography, logo. All values verified directly from the master brandbook (`230918_BaB-Brandbook.pdf`, Stand 18. September 2023) by extracting the source pages and eyedropping the canonical color circles. Cross-checked against three production Adobe XD design files.

**Status legend:**
- ✅ **Verified from brandbook source** — eyedropped from the 230918 master brandbook
- ✅ **Verified from production files** — extracted from production Adobe XD design files
- ⚠️ **Implied / not yet codified** — known to exist but not formally specified

---

## Typography — Silka

✅ **Verified.** Silka is the only brand typeface. Page references below are to `230918_BaB-Brandbook.pdf`.

### Foundry & licensing
- **Foundry:** Atipo Foundry (initially distributed as a Font Squirrel freebie release in 2018)
- **License:** see `Silka_webfont_license.pdf` in Drive (file ID `1dxdML4OMAyrcw09JyqVPqmBOlCGIRNPO`)
- **Font files:** `Silka Fonts.zip` in Drive (file ID `1rq8dzIGxH8GQUBi65XSHYSe1GTb3xbAF`)

### Primary typestyles (S. 7) — main communication
The brandbook says: *"These are the styles we use most often in our communication top level."*

| Weight | Use |
|---|---|
| **Silka Bold** | The dominant headline weight. Most prominent on S. 7. Use for hero claims, OOH headlines, billboard text, social-post headlines, presentation titles. |
| **Silka Black** | Heavier display variant for special emphasis. Less common than Bold. Use sparingly when extra weight is needed. |
| **Silka Regular** | Body copy default. |

### Functional typestyles (S. 8) — when going deeper
The brandbook says: *"When we dive deep into BookaBox on a more functional level of information, we use the displayed styles to structure and organize our content and create clear information hierarchies."*

| Weight | Use |
|---|---|
| **Silka Medium** | Sub-heads, structural labels, mono-caps section labels |
| **Silka Light** | Long-form descriptions, secondary copy |
| **Silka Regular Italic** | Quotes, captions, accents |
| **Silka Light Italic** | Long-form accent text, captions |

### Critical correction from earlier versions of this skill
Earlier drafts named **Silka Black** as the primary headline weight. The 230918 master brandbook puts **Silka Bold first and largest** on the typography page. Silka Bold is the canonical headline weight; Silka Black is a heavier alternative used selectively.

### Webfont implementation

The CSS files in Drive (Stand 2018) use a deprecated naming convention that declares each weight as a separate `font-family` — do not copy that pattern. Use a single `Silka` family with weight variants:

```css
@font-face {
  font-family: 'Silka';
  src: url('/fonts/silka-light.woff2') format('woff2');
  font-weight: 300;
}
@font-face {
  font-family: 'Silka';
  src: url('/fonts/silka-regular.woff2') format('woff2');
  font-weight: 400;
}
@font-face {
  font-family: 'Silka';
  src: url('/fonts/silka-medium.woff2') format('woff2');
  font-weight: 500;
}
@font-face {
  font-family: 'Silka';
  src: url('/fonts/silka-bold.woff2') format('woff2');
  font-weight: 700;
}
@font-face {
  font-family: 'Silka';
  src: url('/fonts/silka-black.woff2') format('woff2');
  font-weight: 900;
}

body { font-family: 'Silka', system-ui, sans-serif; font-weight: 400; }
h1, h2, .display { font-weight: 700; } /* Silka Bold — primary headline */
.heavy { font-weight: 900; }            /* Silka Black — special emphasis */
strong { font-weight: 700; }
```

### Type-scale reference (from brandbook page templates)
These are reference proportions; absolute size scales with medium (poster vs. mobile vs. signage). Keep the relative hierarchy.

| Role | Size / Line-height | Weight |
|---|---|---|
| Topic / section title | 32 pt | Silka Bold |
| Display headline | 3–6× body | Silka Bold (Silka Black for special emphasis) |
| Copy bold | 16 pt / 20 pt | Silka Bold |
| Copy ultra-light | 16 pt / 20 pt | Silka Light |
| Description regular | 14 pt / 20 pt | Silka Regular |
| Mono caps label | small, gray | Silka Medium, letter-spacing positive |

### Fallback stack

```css
font-family: 'Silka', 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
```

Flag the fallback as emergency-only in code comments. Never specify the fallback as primary.

---

## Color — Marketing & Digital

✅ **Verified from brandbook S. 9 master swatches.** Eyedropped at 150 DPI directly from the source page; sub-pixel JPG drift may shift values by 1–2 in any channel — round to nearest tasteful value when implementing.

### Primary colors (S. 9)
The brandbook defines exactly two primary colors.

| Token | Hex | RGB | Use |
|---|---|---|---|
| **Brand White** | `#FFFFFF` | `255, 255, 255` | Light canvas, text on dark |
| **Brand Black** | `#000000` | `0, 0, 0` | Dark canvas, body text on light |

### Secondary colors (S. 9) — grayscale ramp
The brandbook defines an 8-step grayscale ramp. Verified from S. 9 swatches:

| Step | Hex | RGB | Use |
|---|---|---|---|
| Gray 50 | `#F5F5F5` | `245, 245, 245` | Lightest — backgrounds, subtle separators |
| Gray 100 | `#DCDCDC` | `220, 220, 220` | Light dividers, disabled states |
| Gray 200 | `#C0C0C0` | `192, 192, 192` | Light borders |
| Gray 300 | `#A9A9A9` | `169, 169, 169` | Mid-light gray |
| Gray 500 | `#8E8E8E` | `142, 142, 142` | Mid gray |
| Gray 600 | `#656565` | `101, 101, 101` | Stronger UI gray |
| Gray 700 | `#454545` | `69, 69, 69` | Heavy gray, dark text on light surfaces |
| Gray 800 | `#2B2B2B` | `43, 43, 43` | Near-black, soft alternative to pure `#000` |

### Functional colors (S. 9)
The brandbook page is titled *"Functional colors"* and shows four hues. **Important nuance:** the brandbook does not call these "campaign" colors — they're labeled "Functional." But in the OOH and social mockups (S. 13–17, 25), these and additional pinks/coral are clearly used as **highlight backgrounds for campaign work**. The skill treats them as a unified highlight palette governed by Hard Rule #7 (one campaign color per piece).

| Token | Hex | RGB | Use |
|---|---|---|---|
| **Functional Green** | `#0D7A37` | `13, 122, 55` | Success states, confirmations |
| **Functional Red** | `#D6454C` | `214, 69, 76` | The brandbook's red — muted, confident. Distinct from system-error red. |
| **Functional Orange** | `#FF9829` | `255, 152, 41` | Energy, warmth — used in the Fund deck (April 2026) for institutional framing |
| **Functional Blue** | `#689ECC` | `104, 158, 204` | Calm, informational, slightly dusty |

### Highlight / Campaign colors — the extended applied palette
The OOH and social mockups (S. 13–17, 25) introduce additional highlight colors that extend beyond the four functional swatches on S. 9. These are the colors actually used to carry campaigns. **The dominant highlight is Brand Coral Pink** — used on the most iconic billboard mockup (drag queen, S. 13), the social Instagram mockup (S. 25), and the imagery people backgrounds (S. 10).

| Token | Hex | RGB | Source | Use |
|---|---|---|---|---|
| **Brand Coral Pink** ⭐ | `#F25966` | `242, 89, 102` | OOH p13, Social p25, Imagery p10 — eyedropped median | **Primary brand highlight color.** Use for hero campaigns, presentation accents, key social posts, primary OOH backgrounds. The dominant brand-warm color across campaigns. |
| **Brand Yellow** | `#F0C068` | `240, 192, 104` | Imagery p10 (woman with afro) | Warm, optimistic accent |
| **Brand Sand** | `#E0A868` | `224, 168, 104` | OOH p14 (Einhorn), Imagery p10 | Earthy, calm — less aggressive than Coral Pink |
| **Brand Soft Pink** | `#F898A0` | `248, 152, 160` | Imagery p10 (woman thinking), OOH p15 | Softer, pastel variant of Coral Pink for secondary surfaces |
| **Brand Dusty Rose** | `#E090A8` | `224, 144, 168` | Imagery p10 (woman with glasses), OOH p17 | Cooler pink — for variety alongside Coral Pink |
| **Brand Teal** | `#307878` | `48, 120, 120` | Imagery p10 (man in orange shirt) | Deep, contemplative — counterweight to warm pinks |
| **Brand Bright Blue** | `#00A0E0` | `0, 160, 224` | Imagery p10 (man in blue), OOH p16 | Cyan-ish bright blue. Distinct from `#689ECC` Functional Blue. |
| **Brand Webbanner Green** | `#4CCE93` | `76, 206, 147` | Web mockup p22 | Lively mint-green for digital ads. Distinct from `#0D7A37` Functional Green. |

### Hierarchy of use
1. **Default canvas** is Brand Black or Brand White. No other colors as page-background outside campaign work.
2. **Body text** is Brand Black on light, Brand White on dark. Never gray as primary text.
3. **Single campaign color per piece** (Hard Rule #7). For most consumer-facing work, the default is **Brand Coral Pink `#F25966`**. Use the others when context calls for a different feel:
   - **Coral Pink `#F25966`** — default brand-warm highlight, presentations, social, OOH
   - **Functional Orange `#FF9829`** — institutional / financial / investor framing (Fund deck precedent)
   - **Bright Blue `#00A0E0`** — calm, informational, status surfaces
   - **Sand `#E0A868`** — earthy, less aggressive contexts
   - **Webbanner Green `#4CCE93`** — digital ads, web banners
   - **Teal, Soft Pink, Dusty Rose, Yellow** — supporting roles when a campaign needs a distinct flavor
4. **Functional colors are not aesthetic.** Use Functional Green `#0D7A37` only for success states; never for decoration. Use Functional Red `#D6454C` for confirmation/alerts when needed; never as a Coral Pink substitute.

### CSS custom properties

```css
:root {
  /* Primary */
  --brand-black: #000000;
  --brand-white: #FFFFFF;

  /* Grayscale ramp (S. 9 secondary colors) */
  --gray-50:  #F5F5F5;
  --gray-100: #DCDCDC;
  --gray-200: #C0C0C0;
  --gray-300: #A9A9A9;
  --gray-500: #8E8E8E;
  --gray-600: #656565;
  --gray-700: #454545;
  --gray-800: #2B2B2B;

  /* Highlight / campaign colors — pick ONE per piece (Hard Rule #7) */
  --brand-coral-pink:    #F25966;  /* PRIMARY HIGHLIGHT — most BookaBox campaigns */
  --brand-orange:        #FF9829;  /* institutional / financial framing */
  --brand-bright-blue:   #00A0E0;  /* calm, informational */
  --brand-sand:          #E0A868;  /* earthy, soft */
  --brand-webbanner-green: #4CCE93; /* digital ads */
  --brand-teal:          #307878;
  --brand-soft-pink:     #F898A0;
  --brand-dusty-rose:    #E090A8;
  --brand-yellow:        #F0C068;

  /* Functional — system states only */
  --func-green:  #0D7A37;
  --func-red:    #D6454C;
  --func-orange: #FF9829;
  --func-blue:   #689ECC;
}
```

### Reference image
See `references/brandbook-images/p09-colors.jpg` for the brandbook color page itself. See `p10-imagery-people.jpg` for the people-imagery palette and `p13-ooh-coral-pink.jpg` for a full-bleed Coral Pink application.

---

## Color — Interior / Architecture (Locations)

✅ **Verified from `230406_RAL_Color Definition.pdf`** (Drive file `1bag_tNi8n7XymhL5gla0JHg7fJeWI-gd`) and brandbook S. 38.

> ⚠️ **Wichtiger Hinweis aus dem Color-PDF:** RAL-Farben mit "RAL Fächer K5 Classic matt" überprüfen. Bildschirmeindruck weicht vom Original ab.

### Base colors (canonical interior palette, brandbook S. 38)
| Name | RAL Code |
|---|---|
| **Reinweiß (matt)** — primary white | RAL 9010 |
| **Cremeweiß** — soft warm white | RAL 9001 |
| **Anthrazitgrau** — primary dark | RAL 7016 |
| **Schwarz** — full black accent | RAL 9005 (or pure black) |

### Extended whites
| Name | RAL Code |
|---|---|
| Signalweiß | RAL 9003 |
| Verkehrsweiß | RAL 9016 |
| Reinraumweiß | RAL 9012 |
| Perlweiß | RAL 1013 |
| Grauweiß | RAL 9002 |
| Papyrusweiß | RAL 9018 |

### Extended grays
| Name | RAL Code |
|---|---|
| Kieselgrau (Pebble Grey) | RAL 7032 |
| Seidengrau | RAL 7044 |
| Schwarzgrau | RAL 7021 |

### Materials
- **Wood-based wall elements** — wooden slat panels (specific species not standardized)
- **Plant-based wall elements** — moss-green accent (live or preserved moss)

### Use rule
The interior palette stays in the architectural domain. Do not pull RAL into digital marketing as the primary palette — these are reference for the built environment. Marketing/digital colors are above.

---

## Logo

✅ **Verified from brandbook S. 6.**

### Four official variants
The brandbook page 6 shows the logo in four equal-status variants:

1. **Wordmark on light** — `BookaBox.com` in Silka Bold, black on white background
2. **Wordmark on dark** — `BookaBox.com` in Silka Bold, white on black background
3. **Pill on light** — `BookaBox.com` in Silka Bold inside a black rounded-pill capsule, used as CTA button on light surfaces
4. **Pill on dark** — `BookaBox.com` in Silka Bold inside a white rounded-pill capsule, used as CTA button on dark or campaign-color surfaces

The pill variant is **not just a button style** — it's an officially sanctioned alternate logo form. It appears as a CTA-button on every OOH mockup in the brandbook.

### Pill specifications
- Shape: rounded-rectangle "pill" with full-radius end caps (`border-radius: 999px` in CSS, or `border-radius: 50%` of the height)
- Padding: roughly 0.6× height horizontal, 0.3× height vertical
- Wordmark: `BookaBox.com` set in Silka Bold, vertically centered

### "BaB" avatar (S. 25 — Social Media)
For social media profile avatars, the wordmark abbreviates to **`BaB`** (not "BoB" — the lowercase `a` is the middle letter, since it's the abbreviation of **B**ook**a**Box). Set in Silka Bold inside a circular black-on-white or white-on-black mark. Visible in the Instagram mockup on S. 25.

### Source files in Drive
- `BaB_Logo_black.svg` (path-based, currentColor fill) — Drive file `1ECzybSNK6UpMEpgoDan6r3xJr0_uk62M`
- White and on-black PNG variants in same folder
- Source `BaB-BRandbook_Graphics.ai` — Drive file `1vBU3LSZ6JEIEcMKumMI0MU3zspPpI2x5`

The SVG inherits color from `currentColor`, so it can be tinted via CSS:
```css
.logo svg path { fill: black; }              /* default */
.dark-bg .logo svg path { fill: white; }     /* on dark canvas */
.brand-pill { background: black; color: white; padding: 0.3em 0.7em; border-radius: 999px; font-weight: 700; }
```

### Reference image
See `references/brandbook-images/p06-logo.jpg` for the four logo variants. See `p25-detail-bab-avatar.jpg` for the BaB social avatar in context.

---

## Iconography

⚠️ **Not formally codified.** The brandbook does not define an icon system. The Fund deck uses simple monochromatic line icons but does not specify a library or stroke style.

**Provisional recommendation** until a system is defined: use **Lucide Icons** (https://lucide.dev) at consistent stroke width (1.5 px or 2 px), in the active campaign color or grayscale.

---

## Spacing & Layout

⚠️ **Not formally codified.** The brandbook has no documented spacing scale, grid, or layout token set.

**Provisional approach** — match the visual conventions of existing materials:
- Generous whitespace (~5–8% of canvas as outer padding on slides and posters)
- Headlines align to a left margin; body content tracks from the same axis
- Stat cards center-align on their own axis, not the page axis
- Suggest a 4-pt or 8-pt base unit and a 12-column grid for web until something is decided

---

## Reference images included with this skill

`references/brandbook-images/` contains key brandbook pages as JPGs for visual reference at design time:

- `p06-logo.jpg` — four logo variants
- `p07-typography-primary.jpg` — Silka Bold / Black / Regular
- `p08-typography-functional.jpg` — Silka Medium / Light / Italics
- `p09-colors.jpg` — Primary / Secondary / Functional palette
- `p10-imagery-people.jpg` — 8 canonical portrait motives with backgrounds
- `p11-imagery-product.jpg` — 8 box-size renderings
- `p13-ooh-coral-pink.jpg` — flagship Coral Pink billboard
- `p14-ooh-sand.jpg` — Sand billboard
- `p15-ooh-soft-pink.jpg` — Soft Pink billboard
- `p16-ooh-bright-blue.jpg` — Bright Blue billboard
- `p17-ooh-rose.jpg` — Dusty Rose billboard
- `p22-webbanner-green.jpg` — Webbanner Green application
- `p25-social-instagram.jpg` — Instagram post in Coral Pink
- `p25-detail-bab-avatar.jpg` — close-up of the `BaB` social avatar
- `p38-interior-colors.jpg` — interior base-color palette and materials
- `p47-wall-typography.jpg` — wall-typography patterns at locations

Reach for these when a design decision needs visual confirmation.
