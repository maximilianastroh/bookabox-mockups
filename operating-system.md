# BookaBox Operating System

> Single Source of Truth · Living Document · Stand: Mai 2026 · Owner: Max

**



    BookaBox · Master Reference · 2026 Q2

# Operating System


Ein Dokument für Tools, AI-Agenten, Team-Workflows und Datenablage. Wer arbeitet wo, was liegt wo, wann läuft was. Die einzige Übersicht, an die wir uns halten.


      Stand**03. Mai 2026
      **Owner**Max Astroh (CEO/CTO)
      **Master-File**bookabox-knowledge/operating-system.md
      **Version**v1.0





    Inhalt

      - **Tech-Stack** — alle Technologien

      - **Architektur** — 6-Tier-Modell

      - **AI-Agenten** — 6 Agenten + Status

      - **Team** — wer arbeitet wo

      - **Datenablage** — GitHub vs. Drive vs. Odoo

      - **File Naming** — Standard für alle Systeme

      - **Workflows** — typische Szenarien

      - **Roadmap** — 16-Wochen-Plan

      - **Cleanup-Plan** — was passiert mit dem Chaos







      § 01

## Tech-Stack

      15 Kerntechnologien


Das ist alles, was wir nutzen. Punkt. Wenn ein Tool hier nicht steht, gehört es nicht in den Stack — entweder reinverhandeln oder weglassen.


      AI Layer · Reasoning & Voice

        ClaudePrimäre Reasoning-Engine. Alle Agenten, alle Sessions.
        Whispr FlowVoice-to-Text Input · Diktieren in Claude statt tippen. macOS/iOS.
        ElevenLabsVoice-Synthesis für Twilio. DE/EN.
        PaperclipAgent-Orchestrator. CEO-Agent läuft hier.
        ChatGPTVerworfen — Claude-only.




      Hub Layer · Data & Orchestration

        OdooERP & Data Lake · 100 GmbHs · System of Record.
        N8NWorkflow-Orchestrator. Hetzner CX21 (Setup geplant).




      Customer Channels

        TwilioVoice-Telefonie 24/7.
        WhatsAppMessaging-Bot (FastAPI auf Railway, Migration nach N8N).
        GmailE-Mail-Eingang → Odoo Helpdesk.
        Google AdsPaid Acquisition · GCLID-Tracking.
        Microsoft AdsPaid Acquisition · MSCLKID-Tracking.
        Google Analytics 4Behavior Tracking · Funnel.




      Physical / IoT Layer

        Gantner GTC/GT7Türen + Box-Locks · Auto-Lock bei Mahnung.
        UniFi ProtectAI-Kameras · Object Detection · Quality-Monitoring.
        Casambi + OtSBeleuchtungssteuerung pro Standort.
        Pudu RoboticsReinigungsroboter · Box-Reinigung nach Auszug.




      Creative & Storage

        GitHubSource of Truth · Code, Skills, Mockups, Briefs.
        Google DriveSharing-Layer · Verträge, Pitches, Externes.
        Adobe (InDesign + PDF Services)Brand-Print-Pipeline · API aktiv.
        AutoCAD APSDWG-Verarbeitung · AI-Floor-Plan-Generierung.
        RailwayHosting · WhatsApp-Agent (Migration zu N8N).







      § 02

## Architektur

      6-Tier-Modell


Daten fließen oben → unten. **N8N orchestriert, Odoo speichert.** Zwei Hubs, zwei Aufgaben. Goldene Regel: Keine externe Kommunikation aus AI-Agenten — alles läuft durch Odoo.



        TIER 1Customer Channels

          **WhatsApp**Messaging
          **Twilio**Voice 24/7
          **Gmail**E-Mail
          **Ads + GA4**Acquisition


      ↓ ↓ ↓ ↓


        TIER 2AI Layer

          **Claude**Reasoning Engine
          **ElevenLabs**Voice-Synthesis
          **Paperclip**Agent-Orchestrator
          **6 AI Agents**CEO live, 5 in Build


      ↓ ↓ ↓ ↓


        TIER 3N8N Hub

          **Workflow Engine**Routing & Webhooks
          **company_id Resolver**Multi-Company-Logik
          **50–150 ms Latenz**Async-First
          **Failure-Isolation**Odoo bleibt up


      ↓ ↓ ↓ ↓


        TIER 4Odoo Data Lake

          **System of Record**100 GmbHs · 1 DB
          **Bank Auto-Import**Reconciliation live
          **E-Mail-Templates**Konsistente Voice
          **Subscriptions + CRM**Kunden, Verträge, Boxen


      ↓ ↓ ↓ ↓


        TIER 5Physical / IoT

          **Gantner**Locks · Auto-Lock
          **UniFi Protect**AI-Kameras
          **Casambi + OtS**Beleuchtung
          **Pudu**Reinigungs-Roboter


      ↓ ↓ ↓ ↓


        TIER 6Creative & Storage

          **GitHub**Source of Truth
          **Google Drive**Sharing-Layer
          **Adobe APIs**Print-Pipeline
          **AutoCAD APS**Floor Plans






### Goldene Regeln


① Alle Kommunikation läuft durch Odoo (keine direkte Gmail/WhatsApp aus Agenten). ② Ein Agent, viele Mandanten — nicht 100 Instanzen. ③ Webhooks sind fire-and-forget mit 5 s Timeout. ④ Customer-facing Aktionen warten nie auf Agenten.







      § 03

## AI-Agenten

      6 Agenten · 1 live · 5 in Build


Jeder Agent hat eine klare Rolle, einen klaren Trigger, klare Odoo-Rechte. Kein Agent redet direkt mit Kunden außer Sales/CR.



        01CEO AgentLive
        Strategic Layer · Aggregation · Anomalie-Erkennung

Tägliches Executive Briefing über alle GmbHs. Anomalie-Erkennung („Hamburg CAC plötzlich +40%"). Strategische Fragen ad-hoc via Paperclip-Chat.

        **+40%**Decision Velocity**0 €**laufende Kosten**Owner:**Max



        02CMO AgentNext · W1–4
        Marketing & Analytics · Ads · CAC · Landing Page

Google + MS Ads Performance täglich. GA4-Analyse pro Standort. CAC-Berechnung pro GmbH. A/B-Tests koordinieren. box_marketing-Modul ready.

        **€800**Ad-Spend gespart/Monat**4h → 0h**Report-Aufwand**Payback:**2-3 Wochen



        03Accounting AgentW5–6
        Finance · Mahnwesen · Reconciliation · Cashflow

Bank-Reconciliation überwachen (Auto-Import läuft). Mahnwesen 3-stufig über `account.followup`. Bei 3. Mahnung → project.task → Standort-Agent. Multi-Company P&L.

        **€2-5k**Recovery/Monat**8h → 30 min**Monatsabschluss**Payback:**2-3 Wochen



        04Sales & CR AgentW7–10
        Voice · Chat · WhatsApp · Bookings · Retention

4 Kanäle: Web-Chat, WhatsApp, Twilio-Voice, E-Mail. Bookings, Retention, Räumungs-Kommunikation. Lebt in N8N (nicht Odoo Live Chat).

        **+15%**Booking-Conversion**24/7**Erreichbarkeit**Payback:**4-6 Wochen



        05Standort-AgentW11–14
        Operations · UniFi · Hausmeister · Räumung

Brücke digital ↔ physisch. UniFi-Augen, Hausmeister-Hände. Übernimmt Räumungen ab Tag 90 vom Accounting. Modell C: Mix intern + Dienstleister.

        **Box-Räumungen**autonom**Revenue-Schutz**direkt**Payback:**3-5 Wochen



        06CTO AgentW15–16
        System Health · Tech Debt · MC Compliance

N8N-Flow-Monitoring. Odoo-Modul-Audit. PR-Scanner für Multi-Company-Compliance. PostgreSQL Health. Odoo 17→18→19 Upgrade-Readiness.

        **0**neue MC-Verstöße**−70%**Custom Code**Hygiene-Layer**präventiv







      § 04

## Team · Wer arbeitet wo

      7 Personen · 4 Tools


Claude ist **Frontend** für alles Schreibende — E-Mails, Tasks, Recherche, Designs. Odoo bleibt **System of Record**. GitHub ist **Master** für Wissen, Code & Skills.




          Person
          Hauptarbeitsplatz
          Sekundär
          Odoo-Zugang




          Max CEO / CTO / Founder
          Claude Design + CodeGitHub
          Drive Sharing
          ✓ Vollzugriff


          Joern Co-Founder · Strategy / Marketing Design
          Claude Design
          GitHub · Drive Pitch-Sharing
          ✓ Vollzugriff


          Katrin Sales & Customer Relations
          Odoo CRM, Helpdesk, Subscriptions
          Claude mit Odoo-MCP für Schreibarbeit
          ✓ Sales/CR-Module


          Sophia SEO Marketing
          Claude · Drive Marketing-Assets
          GitHub für Skill-Management
          ✓ Marketing-Module


          Mats / Ole Assistants
          Claude Frontend für ad-hoc Aufgaben
          —
          ✓ Read-only


          Parmar Team Dev (extern)
          GitHub · eigener Dev-Workflow
          —
          ✓ Tech-Admin


          Reinigung / Bau Externe Ausführende
          WhatsApp, E-Mail (Output von AI-Agenten)
          —
          ✕ kein Zugang






### Wann nutzt wer Claude wofür?


**Katrin/Sophia** für Schreiben, Suchen, Antworten · **Max/Joern** für Strategie, Design, Architektur · **Mats/Ole** für ausführende Tasks. **Routing-Regel:** Wer schreibt einen Task ein? Claude schreibt → Odoo speichert. Niemand schreibt mehr direkt in Odoo, wenn Claude schneller ist.







      § 05

## Datenablage

      3 Schichten · keine Spiegel


Jedes System hat **eine Aufgabe**. Kein System spiegelt das andere. Wenn du nicht weißt wo etwas hingehört, frag dich: *„Muss das versioniert sein, geteilt werden, oder ein Geschäftsvorfall sein?"*



        GitHub
        Master · Source of Truth

Alles was versioniert sein muss. Diff-fähig, durchsuchbar, dauerhaft.


          - Code (alle Repos)

          - Skills für Paperclip / Agenten

          - Briefs & Specs

          - Mockup-Source (Cockpit, Move-Out, Decks)

          - Architektur-Docs (dieses Dokument)

          - Tool-Beschreibungen




        Google Drive
        Working · Sharing

Alles was Externe lesen, kommentieren oder editieren sollen.


          - Verträge (zur Unterschrift)

          - Pitch-PDFs (für Investoren)

          - Bilder, Fotos, Marketing-Assets

          - Excel-Listen für Externe

          - Banken-/Behörden-Dokumente

          - Tom's Pitch zum Kommentieren




        Odoo Documents
        Operativ · Records

Alles was ein Geschäftsvorfall ist und revisionssicher abgelegt werden muss.


          - Mietverträge je Box

          - Eingangs-/Ausgangsrechnungen

          - Kunden-Akten · KYC

          - Bauakten pro Standort

          - Versicherungsfälle

          - Banken-Reporting







### 3 Repos auf GitHub — nicht mehr, nicht weniger


**bookabox-knowledge** · was wissen wir (Briefs, Specs, Tool-Docs, dieses OS-Doc)**
         bookabox-skills** · was können wir (Paperclip-Skills, Agent-Prompts, Workflows)**
         bookabox-mockups** · was gestalten wir (Cockpit, Move-Out, Decks, Frontend-Drafts)







      § 06

## File Naming

      überall gleich


Ein Standard für GitHub, Drive und Odoo. Sortiert sich von selbst, ist auffindbar, hält ewig.


      YYYY-MM-DD_kategorie_kurzbeschreibung_vN.ext

        Beispiele:**
        2026-05-03_pitch_tom-investor_v2.pdf

        2026-05-03_brief_cockpit-redesign.md

        2026-04-28_vertrag_essen-stadtmagazin_signed.pdf





#### Regeln


            - Datum immer vorne** (sortiert sich)

            - Keine Umlaute, keine Leerzeichen → _ oder -

            - Version (v1, v2, final)

            - Lowercase, ASCII only





#### Kategorien (feste Liste)


            - brief · spec · pitch

            - vertrag · rechnung · protokoll

            - mockup · report · analyse

            - (neue Kategorien? → erst hier eintragen)










      § 07

## Workflows

      typische Szenarien


Wie laufen Standard-Aufgaben durchs System? Sechs Beispiele, die 80 % aller Fälle abdecken.



        SZENARIO 01

#### Katrin braucht Hilfe bei einem Accounting-Problem


          - Katrin öffnet **Claude** (mit Odoo-MCP-Zugang)

          - Fragt: „Warum stimmt OP-Liste Essen Q1 nicht?"

          - Claude liest live aus Odoo → analysiert

          - Antwort + Vorschlag → Katrin entscheidet

          - Wenn Buchung nötig: Claude bereitet Eintrag vor, Katrin bestätigt in Odoo





        SZENARIO 02

#### Katrin will Max einen Task einstellen


          - Katrin promptet **Claude**: „Stell Max Task ein: Vertrag Köln gegenzeichnen bis Fr"

          - Claude legt project.task in Odoo an

          - Claude pingt Max (E-Mail über Odoo-Template oder Slack)

          - Max antwortet in Claude → Claude updatet Task in Odoo





        SZENARIO 03

#### Joern baut Pitch Deck für Investor


          - **Claude Design** öffnen → neues Deck

          - HTML-Source pushen nach bookabox-mockups/decks/2026-05-tom-pitch/

          - PPTX/PDF-Export daneben legen

          - Drive-Link generieren → an Tom (Drive ist nur die Verteiler-Schicht)

          - Master bleibt in GitHub





        SZENARIO 04

#### Skill für AI-Agent updaten


          - **Claude Code** öffnen, Repo bookabox-skills

          - Skill-Datei editieren

          - Push → Railway Auto-Deploy → Paperclip lädt neuen Skill

          - Test in Paperclip-Chat





        SZENARIO 05

#### Mahnwesen-Eskalation Tag 0 → Räumung


          - **Tag 0**: Odoo Auto-Lock (Gantner) bei unbezahlter Rechnung

          - **Tag 30/60**: Accounting-Agent Mahnung 1 + 2 (Odoo-Template)

          - **Tag 90**: Mahnung 3 → project.task für Standort-Agent

          - **Tag 104+**: Standort-Agent + Hausmeister räumen, Pudu reinigt





        SZENARIO 06

#### Neuer Chat startet — wo Kontext herholen?


          - Erste Zeile: „Lies bookabox-knowledge/operating-system.md"

          - Bei spezifischem Thema zusätzlich z.B. briefs/cockpit.md

          - Claude liest direkt aus GitHub — **kein Upload, kein ZIP**

          - Session ist sofort kontextualisiert









      § 08

## Roadmap · 16-Wochen-Plan

      ~268h Aufwand · <2 Mon. Payback


Vom heutigen Stand (CEO live) bis Vollausbau aller 6 Agenten. Sequenz folgt ROI und Abhängigkeiten.



        WocheAgentWas passiertAufwandStatus


        Heute
        CEO
        Daily Briefing · Anomalie-Erkennung · Cross-Context Reasoning
        live
        Live


        W 1–4
        CMO
        Ads-Integration · Daily Reports · CAC-Dashboard · box_marketing deploy
        ~52h
        Next


        W 5–6
        Accounting
        Mahnwesen 3-stufig · Reconciliation-Kontrolle · DSO-Reduktion
        ~48h
        Queued


        W 7–10
        Sales & CR
        Voice + Chat + WhatsApp Migration nach N8N · 24/7 Erreichbarkeit
        ~64h
        Queued


        W 11–14
        Standort
        UniFi-Quality-Monitoring · Hausmeister-Tasks · Räumungs-Ausführung
        ~80h
        Queued


        W 15–16
        CTO
        N8N-Health · Odoo Audit · MC-Compliance Scanner · Upgrade-Readiness
        ~24h
        Queued





### Kritische Next Steps


**Diese Woche:** Google Ads Developer Token beantragen (1-3 Werktage Approval). · **Woche 3:** UniFi-API-Credentials aller Standorte sammeln. · **Parallel laufend:** N8N-Setup auf Hetzner CX21.







      § 09

## Cleanup-Plan

      heute machen, sonst driften wir wieder ab


Aktueller Stand: 60 MD-Files in einem Drive-Ordner, 13 Claude-Projekte, kein klares Mapping. Hier der Aufräumweg in 4 Schritten.




          #
          Was
          Aktion
          Ziel
          Files




          1
          **Tech-Architektur-MDs****00_Tech_Overview, 04_Agents, 07_Roadmap, 05_Eskalation, 06_Standort-Agent, 02_Ads-Roadmap, 03_box_marketing
          Konsolidieren in dieses OS-Doc · Originale ablegen
          bookabox-knowledge/
architecture/
          7


          2
          Business-Plan-Kapitel****00_Sparkasse, 01-07_Kapitel, 08_Reminder, Snapshot_KONSOLIDIERT
          Bleiben im Drive (Bank-Einreichung) · 1 Kopie in GitHub
          Drive: 02_Business_Plan/
GitHub: business-plan/
          9


          3
          Buchhaltung & Finanzen****SKR03 BS + Service, Vertragsstruktur, Tilgung, Vorsteuer-Schaden
          In Knowledge-Repo, fest verlinkt mit Odoo-Records
          bookabox-knowledge/
finance/
          6


          4
          Pitch / Investoren****Joern-Pitch, Tom, Shimshon-NOI, Term-Sheets
          Master nach GitHub · PDFs auf Drive für Investor-Sharing
          bookabox-knowledge/
investors/
          8


          5
          Chat-Exports****Architekt-Werkbank, Move-Out, Hannover-Bau, alte Sessions
          Archivieren · nicht löschen · für Audit-Trail
          bookabox-knowledge/
_archive/chat-exports/
          12


          6
          Meta-Files****CLEANUP_ANLEITUNG, Snapshot-README, Drive-Ablage-Prompt
          Behalten als Referenz für künftige Cleanups
          bookabox-knowledge/
_meta/
          8


          7
          Duplikate****Files mit „(1)"-Suffix
          Löschen — neuere Version behalten
          —
          ~10






### 4-Schritt-Cleanup heute


① GitHub:** 3 Repos anlegen (knowledge, skills, mockups). · ② **Drive:** Neue Ordnerstruktur nach §05 anlegen, Files mit File-Naming aus §06 umbenennen, Duplikate löschen. · ③ **Claude-Projekte:** 13 → 3 reduzieren („BAB Knowledge", „BAB Design", „BAB Engineering"). · ④ **OS-Doc als bookabox-knowledge/operating-system.md committen** — ab dann startet jeder Chat mit „Lies operating-system.md".






    bookabox-knowledge/operating-system.md · v1.0 · 03.05.2026
    Owner: Max Astroh · Co: Joern
