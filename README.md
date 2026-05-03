# BookaBox Brand Skill — Final Bundle

This is the complete `bookabox-brand` skill bundle, ready to upload to Claude. All values verified directly from the master brandbook (`230918_BaB-Brandbook.pdf`).

## What changed in this final version

- ✅ **Coral Pink `#F25966`** confirmed as the primary brand-warm highlight (the iconic billboard/Instagram color — see brandbook S. 13, S. 25, imagery S. 10)
- ✅ **Silka Bold** corrected as the canonical headline weight (earlier drafts incorrectly said Silka Black)
- ✅ **All 18 brand-relevant hex codes** eyedropped from brandbook S. 9 source page
- ✅ **Logo Pill variant** documented — both as alternate logo form and CTA-button pattern
- ✅ **`BaB` social avatar** correctly spelled (not `BoB`) — verified against brandbook S. 25 Instagram mockup
- ✅ **Wall-typography patterns** from brandbook S. 47 added to voice guide
- ✅ **8 canonical portrait motives** verified (brandbook S. 10) with backgrounds + persona mapping
- ✅ **16 brandbook reference images** included as visual fallbacks for design decisions

## Contents

```
bookabox-brand/
├── SKILL.md                              # Skill entry point (Claude reads this first)
├── README.md                             # This file
└── references/
    ├── brand-guide.md                    # Authoritative brand rules
    ├── voice-and-tone.md                 # Two-pole voice, headline patterns, wall typography
    ├── review-checklist.md               # 12-section audit for existing work
    ├── creation-checklist.md             # Pre-flight for new work
    ├── imagery-index.md                  # 8 canonical motives + Drive locations
    ├── marketing-examples.md             # User journeys, personas, layout patterns
    ├── template-pitchdeck.md             # Pitch-deck pattern (Fund deck Apr 2026)
    ├── tokens.md                         # Implementation tokens — Silka, hex codes, RAL
    └── brandbook-images/                 # 16 reference JPGs from the master brandbook
        ├── p06-logo.jpg
        ├── p07-typography-primary.jpg
        ├── p08-typography-functional.jpg
        ├── p09-colors.jpg
        ├── p10-imagery-people.jpg
        ├── p11-imagery-product.jpg
        ├── p13-ooh-coral-pink.jpg
        ├── p14-ooh-sand.jpg
        ├── p15-ooh-soft-pink.jpg
        ├── p16-ooh-bright-blue.jpg
        ├── p17-ooh-rose.jpg
        ├── p22-webbanner-green.jpg
        ├── p25-social-instagram.jpg
        ├── p25-detail-bab-avatar.jpg
        ├── p38-interior-colors.jpg
        └── p47-wall-typography.jpg
```

## How to upload to Claude

1. In Claude (web or app), open **Settings → Capabilities → Skills**.
2. If a `bookabox-brand` skill already exists, **delete it** or use the "Replace" / "Update" option.
3. Click **Upload skill** and select the entire `bookabox-brand` folder (or upload as a zip).
4. Claude will index `SKILL.md` first; the references load on demand when the skill needs them.
5. Test: in a new chat, ask Claude to "review this BookaBox copy" and paste any short paragraph. The skill should activate automatically.

## Source provenance

All Markdown files distill from these primary sources:

| Markdown file | Distilled from |
|---|---|
| `brand-guide.md` | `230918_BaB-Brandbook.pdf` (full, S. 1–66) + Vermieter-PDF + Fund deck Apr 2026 |
| `voice-and-tone.md` | Brandbook S. 13–17, 22, 25, 47 (OOH + wall typography) + Fund deck |
| `review-checklist.md` | Derived from brand-guide + voice-and-tone + tokens |
| `creation-checklist.md` | Derived from brand-guide + voice-and-tone + tokens |
| `imagery-index.md` | Brandbook S. 10–11 (8 motives + 8 box-size renderings) |
| `marketing-examples.md` | `230719_Marketing.pdf` |
| `template-pitchdeck.md` | BookaBox.com Fund deck (April 2026) |
| `tokens.md` | Brandbook S. 6 (logo), S. 7–8 (typo), S. 9 (colors), S. 38 (interior), + RAL Color Definition PDF + 3 production XD files |

## Known gaps

These are flagged inside the references but worth knowing up front:

1. **Persona-to-Motiv-filename mapping** — brandbook shows 8 motives on S. 10; Drive has 11 Motiv files. Mapping needs a 30-minute review (see `imagery-index.md`).

2. **English voice parallels** for German idioms — flagged but not yet populated.

3. **Email signature templates, SMS tone, and several surface-specific tone rules** — not yet defined.

4. **Spacing & grid system** — not codified; provisional 4-pt or 8-pt base recommended.

5. **Iconography** — no defined system; Lucide is the provisional recommendation.

When you fix any of these, update the relevant `.md` file and re-upload the skill bundle.

## Updating the skill later

Whenever you want to update the skill:

1. Edit the relevant `.md` file locally (or directly in the Claude skill editor if the UI allows it)
2. Re-upload the folder, replacing the old version
3. The next conversation that triggers the skill will use the updated content

If you make a substantial change to `SKILL.md` — especially the `description` field at the top — note that it affects when Claude auto-loads the skill. The current description is broad on purpose: any BookaBox creative or marketing task should trigger it.
