# Cleanup Handover · Design → Code

**Datum:** 03.05.2026
**Von:** Claude Design Session (Max)
**An:** Claude Code Session, Repo `bookabox-knowledge`, Branch `main`
**Ziel:** §09 Cleanup-Plan ausführen — 60 MD-Files aus Drive sortieren, 13 Claude-Projekte → 3 reduzieren

---

## Voice-Prompt für Claude Code (zum Diktieren am Anfang der Code-Session)

> *Hi Claude. Cleanup-Session. Lies operating-system.md im aktuellen Repo zur Orientierung — besonders §05 Datenablage, §06 File Naming, §09 Cleanup-Plan. Lies auch _meta/cleanup-handover-2026-05-03.md (das hier) für Kontext aus der vorherigen Design-Session. Dann warte auf meine Drive-File-Liste. Erstelle eine Mapping-Tabelle als _meta/cleanup-2026-05-03.md — pro Datei: aktueller Name, neue Kategorie, neuer Name nach §06, Ziel-Ablage (Drive-Pfad oder GitHub-Repo), Aktion (behalten / umbenennen / verschieben / löschen). Nichts ausführen ohne mein OK. Nach meinem OK pro Block: ausführen für GitHub-Migrationen, Drive-Aktionen markierst du als "manuell durch Max".*

---

## Status heute (was bereits steht)

### ✅ Erledigt

- `bookabox-knowledge` Repo live (privat) mit:
  - `README.md` (Index)
  - `operating-system.md` v1.1 (mit §10 Voice First Workflow)
  - `briefs/2026-05-cockpit-redesign.md`
  - `notebooklm/bab-os-briefing.md`
- `bookabox-mockups` Repo bereinigt
- §10 Voice First Workflow als OS-Sektion etabliert
- Inbox-Pattern (`bookabox-mockups/_inbox/`) als Brücke Design ↔ Code dokumentiert

### ⏳ Offen (diese Session)

- 60 MD-Files in Google Drive sortieren
- 13 Claude-Projekte auf 3 reduzieren (BAB Knowledge, BAB Design, BAB Engineering)
- Duplikate mit "(1)"-Suffix löschen

### ⏳ Offen (Folgeagenda)

- Google Ads Developer Token beantragen (W1, kritisch — 1-3 Werktage Wartezeit)
- NotebookLM-Podcast aus `notebooklm/bab-os-briefing.md` generieren → an Joern
- CMO-Agent W1-4 starten (nach Cleanup)

---

## Cleanup-Kategorien aus §09 (zur Erinnerung)

| # | Kategorie | Aktion | Ziel |
|---|---|---|---|
| 1 | Tech-Architektur-MDs (00_Tech_Overview, 04_Agents, 07_Roadmap, 05_Eskalation, 06_Standort-Agent, 02_Ads-Roadmap, 03_box_marketing — 7 Files) | Konsolidieren in OS-Doc · Originale ablegen | `bookabox-knowledge/architecture/` |
| 2 | Business-Plan (00_Sparkasse, 01-07_Kapitel, 08_Reminder, Snapshot — 9 Files) | Drive bleibt Master für Bank · 1 Kopie GitHub | Drive: `02_Business_Plan/` + GitHub: `business-plan/` |
| 3 | Buchhaltung (SKR03 BS + Service, Vertragsstruktur, Tilgung, Vorsteuer-Schaden — 6 Files) | In Knowledge-Repo · verlinkt mit Odoo-Records | `bookabox-knowledge/finance/` |
| 4 | Pitch / Investoren (Joern-Pitch, Tom, Shimshon-NOI, Term-Sheets — 8 Files) | Master nach GitHub · PDFs auf Drive | `bookabox-knowledge/investors/` |
| 5 | Chat-Exports (Architekt-Werkbank, Move-Out, Hannover-Bau, alte Sessions — 12 Files) | Archivieren · nicht löschen | `bookabox-knowledge/_archive/chat-exports/` |
| 6 | Meta-Files (CLEANUP_ANLEITUNG, Snapshot-README, Drive-Ablage-Prompt — 8 Files) | Behalten als Referenz | `bookabox-knowledge/_meta/` |
| 7 | Duplikate (Files mit "(1)") — ~10 Files | Löschen — neuere Version behalten | — |

---

## File-Naming-Standard aus §06 (zur Erinnerung)

`YYYY-MM-DD_kategorie_kurzbeschreibung_vN.ext`

Kategorien (feste Liste): `brief`, `spec`, `pitch`, `vertrag`, `rechnung`, `protokoll`, `mockup`, `report`, `analyse`

Regeln:
- Datum vorne (sortiert sich)
- Keine Umlaute, keine Leerzeichen → `_` oder `-`
- Lowercase, ASCII only
- Version (`v1`, `v2`, `final`)

---

## Output-Format der Cleanup-Tabelle

Code soll erstellen: `_meta/cleanup-2026-05-03.md` mit Tabelle:

```markdown
| Aktueller Name | Kategorie | Neuer Name | Ziel | Aktion | Status |
|---|---|---|---|---|---|
| 00_Tech_Overview.md | 1 Architektur | 2026-05-03_brief_tech-overview.md | bookabox-knowledge/architecture/ | github-migrate | ⏳ |
| Joern-Pitch_v3.md | 4 Pitch | 2026-04-15_pitch_joern-investor_v3.md | bookabox-knowledge/investors/ | github-migrate | ⏳ |
| Pitch_v3 (1).md | 7 Duplikat | — | — | delete | ⏳ |
```

Nach Approval pro Block → Status auf ✅, Code committed.

---

## Ablauf der Code-Session

1. **Max diktiert Voice-Prompt oben**
2. **Max gibt Drive-File-Liste** (Screenshot oder Paste)
3. **Code erstellt Mapping-Tabelle** in `_meta/cleanup-2026-05-03.md`
4. **Max reviewt** — pro Block "OK" oder "Änderung X"
5. **Code führt GitHub-Migrationen aus** (Drive macht Max manuell, Code markiert nur)
6. **Code commitet final cleanup-2026-05-03.md** mit ✅ Status
7. **Code reduziert Claude-Projekte** → kann nicht direkt, gibt Liste der zu archivierenden Projekte aus, Max archiviert manuell auf claude.ai

---

## Wichtige Constraints

- **Drive-API:** Code hat keinen Zugriff. Drive-Aktionen → Max macht manuell, Code dokumentiert nur.
- **Claude-Projekte:** Code kann nicht löschen. Liste raus, Max archiviert.
- **GitHub:** Code hat Schreibrechte auf alle bookabox-* Repos. Migrationen direkt.
- **Originale nicht löschen:** Vor Migration Originale nach `_archive/` — Sicherheitsnetz.
- **Atomic Commits:** Pro Cleanup-Kategorie ein Commit. Nicht alles auf einmal.
