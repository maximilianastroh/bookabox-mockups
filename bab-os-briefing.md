# BookaBox Operating System — Audio-Briefing

**Format:** Optimiert für NotebookLM-Podcast-Generierung (Audio Overview / Deep Dive)
**Sprache:** Deutsch — wenn NotebookLM auf Englisch generiert, wird's automatisch übersetzt
**Länge der Quelle:** ~12 Min Lesezeit · Erwartete Podcast-Länge: 15-20 Min
**Zielgruppe:** Co-Founder, Investoren, Team-Member, technische Partner
**Tonalität:** Konkret, ehrlich, zukunftsgerichtet — keine Buzzword-Soße

---

## Warum dieses Dokument existiert

BookaBox baut die erste vollständig AI-betriebene Self-Storage-Operation Europas. 100 GmbHs, eine Marke, ein Operating-System. Wir sind 4 Menschen plus 6 AI-Agenten. Ende 2026 wollen wir dort sein, wo Branchenriesen mit 50 Mitarbeitern stehen — mit dem gleichen Team, das heute den Laden schmeisst.

Dieses Doc beschreibt zwei Dinge:

1. **Wo wir heute stehen** — der reale Tech-Stack, die laufenden Agenten, die etablierten Workflows
2. **Wo wir 2026/27 hingehen** — Voice-only Operations, AI-Glasses für Quality-Management, Spatial Coding, Design-Reviews ohne Tastatur

Beide Welten existieren gleichzeitig. Heute machen wir einiges noch klassisch (Tippen, Klicken, Tabs wechseln). Morgen sprechen wir mit dem System und schauen es an. Der Übergang ist fließend, und genau diesen Übergang beschreiben die folgenden Sektionen.

---

## Teil 1 · Der heutige Tech-Stack

15 Kerntechnologien, kategorisiert nach Funktion. Wenn ein Tool hier nicht steht, gehört es nicht in den Stack. Diese Disziplin ist wichtig — sonst verliert man sich in 50 SaaS-Tools, die niemand mehr durchblickt.

### AI Layer · Reasoning & Voice

- **Claude (Anthropic):** Primäre Reasoning-Engine. Alle Agenten laufen auf Claude. Alle internen Sessions nutzen Claude. Wir haben uns bewusst gegen ChatGPT entschieden — eine Engine, ein Verhaltensmodell, eine Tonalität.
- **Whispr Flow:** Voice-to-Text-Input. Statt zu tippen, diktieren wir Briefs, Specs, Prompts in Claude. Auf macOS und iOS. Das ist der Einstieg in unsere "Voice-First"-Strategie — und der Schritt, der die meisten Mitarbeiter am schnellsten produktiv macht.
- **ElevenLabs:** Voice-Synthesis für Twilio-Anrufe. Deutsche und englische Stimmen für unseren Voice-Agenten — der Kunden 24/7 anruft und annimmt.
- **Paperclip:** Agent-Orchestrator. Hier läuft der CEO-Agent, der Aufgaben an die Spezialisten-Agenten delegiert.

### Hub Layer · Data & Orchestration

- **Odoo:** Unser ERP und Data Lake. 100 GmbHs sind hier abgebildet. Verträge, Buchhaltung, Helpdesk, Inventory. **Goldene Regel: Odoo ist System of Record. Keine Daten existieren außerhalb.**
- **N8N:** Workflow-Orchestrator (in Setup auf Hetzner). Verbindet alles mit allem. Wenn ein Twilio-Anruf reinkommt, transkribiert wird, durch Claude analysiert wird und dann eine Odoo-Aktion auslöst — das macht N8N.

### Customer Channels

- **Twilio:** Voice-Telefonie 24/7. Kunden können jederzeit anrufen, der AI-Agent nimmt ab.
- **WhatsApp Business:** Messaging-Bot. Aktuell als FastAPI-Service auf Railway, Migration zu N8N geplant.
- **Gmail:** E-Mail-Eingang fließt direkt in Odoo Helpdesk.
- **Google Ads + Microsoft Ads + Google Analytics 4:** Paid Acquisition mit GCLID/MSCLKID-Tracking, Funnel-Analyse.

### Physical / IoT Layer

Hier wird's spannend, weil hier die digitale und die physische Welt zusammenkommen:

- **Gantner GTC/GT7:** Türen und Box-Locks. Auto-Lock bei Mahnung — wenn der Kunde nicht zahlt, schließt die Box automatisch.
- **UniFi Protect:** AI-Kameras mit Object Detection. Wir nutzen sie für Quality-Monitoring (Sauberkeit, Leerstand-Verifikation).
- **Casambi + OtS:** Beleuchtungssteuerung pro Standort.
- **Pudu Robotics (geplant):** Reinigungsroboter, die Boxen nach Auszug autonom reinigen. Der Move-out-Flow endet mit "Roboter ist im Zielraum" und beginnt automatisch das nächste Onboarding.

### Creative & Storage

- **GitHub:** Source of Truth für Code, Skills, Mockups, Briefs. Wir haben drei Repos: `bookabox-cockpit`, `bookabox-mockups`, `bookabox-skills` — und neu: `bookabox-knowledge` als zentrale Wissensbasis.
- **Google Drive:** Sharing-Layer für Verträge, Pitches, externe Stakeholder.
- **Adobe (InDesign + PDF Services):** Brand-Print-Pipeline, API-gestützt.
- **AutoCAD APS:** DWG-Verarbeitung für AI-generierte Floor-Plans.
- **Railway:** Hosting. WhatsApp-Agent, Migration zu N8N läuft.

---

## Teil 2 · Die sechs AI-Agenten

Jeder Agent hat einen klaren Job, einen Owner und eine messbare KPI.

1. **CEO-Agent** — Strategischer Orchestrator. Liest tägliche Reports, verteilt Aufgaben, eskaliert was Max sehen muss. Owner: Max. KPI: Time-to-Decision.
2. **Voice-Agent (Twilio + ElevenLabs):** Nimmt 24/7 Anrufe an, qualifiziert, bucht Termine, leitet weiter. KPI: Call-to-Booking-Rate.
3. **WhatsApp-Agent:** Asynchroner Sales- und Support-Kanal. KPI: Response-Time, Conversion.
4. **Cockpit-Agent (Ask AI):** Im neuen Cockpit eingebaut. Antwortet auf Voice-Anfragen wie "Wie war der Mai 2025 vs. 2024?". KPI: Self-Service-Rate.
5. **Quality-Agent (in Aufbau):** Liest UniFi-Kamera-Streams, erkennt Probleme (Müll, Schäden, leere Boxen), öffnet Tickets in Odoo. KPI: Issue-Detection-Latency.
6. **Move-out-Agent:** Vollautomatischer End-to-End-Flow für Kündigungen. Vom Kunden-Trigger bis Final-Cleaning-Robot.

---

## Teil 3 · Das Team und wer was macht

**Max** — CEO, CTO, Founder. Vollzugriff überall. Nutzt Claude Design für Mockups, Claude Code für Implementation, GitHub für alles.

**Joern** — Co-Founder, Strategy, Marketing, Design. Claude Design + GitHub-Read-Access. Pitch-Decks, Brand-Material, Investorenkommunikation.

**Jasmin** — Operations & Knowledge-Base-Owner (in Onboarding). Pflegt das Knowledge-Repo. Sicht auf alle Briefs, Specs, Workflows. Erste Person, die sich um Datenqualität kümmert.

**Katrin** — Accounting. Odoo-Vollzugriff für Finanzen. Eskalationspfad bei Buchungsfragen.

---

## Teil 4 · Die heutigen Standard-Workflows

Sechs Szenarien, die wir täglich oder wöchentlich machen. Alle laufen über GitHub als Mitte:

1. **Joern baut Pitch-Deck:** Claude Design öffnen, Deck bauen, HTML-Source nach `bookabox-mockups/decks/...` pushen, PDF-Export daneben legen.
2. **Skill-Update für AI-Agent:** Claude Code öffnen, Skill-Datei in `bookabox-skills` editieren, push → Railway Auto-Deploy → Paperclip lädt neuen Skill innerhalb von Minuten.
3. **Katrin hat Accounting-Frage:** Schreibt in Odoo-Helpdesk, AI-Agent versucht Auto-Antwort, eskaliert an Max wenn unklar.
4. **Cockpit-Anpassung:** Brief in `bookabox-knowledge/briefs/` ablegen, Claude Design erstellt Mockup, Claude Code implementiert in Cockpit-Repo, Deploy.
5. **Standort-Onboarding:** Floor-Plan via AutoCAD APS, Boxen-Inventar in Odoo, Türen über Gantner aktivieren, UniFi-Kameras kalibrieren — Schritt-für-Schritt-Workflow in N8N.
6. **Move-out:** Kunde kündigt → Voice-Agent bestätigt → Final-Inspection via Kamera → Roboter reinigt → Box wieder verfügbar.

---

## Teil 5 · Die Zukunft — Voice-First Operations

Hier wird's spekulativer, aber konkreter als man denkt. Wir bauen aktiv darauf hin. Drei Szenarien, die in 12-18 Monaten Alltag sein werden:

### Szenario A · Quality-Management mit Voice-only und AI-Brille

**Heute:** Max oder Operations-Lead fährt einmal pro Quartal an einen Standort, geht durch, macht Fotos, schreibt Notizen, tippt das später in einen Report.

**2026/27:** AI-Brille auf (Meta Ray-Ban Display, Apple Vision oder Ähnliches). Mitarbeiter — egal ob Max, Jasmin oder ein externer QM-Auditor — geht durch den Standort. Spricht laut: *"Box B-12, der Boden ist verschmutzt, Lampe flackert."* Die Brille:

- Filmt automatisch den Bereich
- Transkribiert die Aussage über Whispr-Tech
- Erkennt durch Computer Vision die Box-Nummer aus dem Türschild
- Loggt das Issue direkt in Odoo Helpdesk mit Foto, Geo-Koordinate, Box-ID
- Triggert ggf. den Quality-Agent zur Eskalation

**Konsequenz:** Ein Audit dauert nicht mehr 4 Stunden Walk + 2 Stunden Tippen, sondern 90 Minuten Walk und alles ist dokumentiert. Wir können Audits **wöchentlich statt quartalsweise** machen, ohne Mehraufwand. Quality-Score eines Standorts wird zur Live-Metrik.

**Was es dafür braucht:**
- AI-Brille mit Always-On-Camera + Voice-Capture
- N8N-Endpoint für "Issue from Field"
- Odoo-Mapping von Box-Nummer zu Standort-Asset
- Pre-trained Vision-Model für Standort-typische Probleme (Müll, Schäden, Beleuchtung)

### Szenario B · Coding mit Voice-only und AI-Brille

**Heute:** Max sitzt am MacBook, schreibt in Claude Code Prompts, reviewed Diffs, pusht.

**2026/27:** Max sitzt im Café, hat Brille auf, sagt: *"Claude, im Cockpit-Repo: füge auf der Burn-Run-Karte einen Toggle für Quartal-vs-Jahr-Ansicht hinzu, halte dich an die Tweaks-Konvention."* Die Brille:

- Zeigt den relevanten Codebereich als overlay-Diff
- Max nickt oder sagt *"approve"* oder *"ändere folgendes..."*
- Push erfolgt sprachgesteuert
- Deploy-Status wird ihm visuell ins Sichtfeld eingeblendet

**Konsequenz:** Coding wird zu einer **konversationellen Tätigkeit**. Die Tastatur ist nur noch für die seltenen Fälle nötig, in denen man Pixel-genau formulieren muss. Iterationsgeschwindigkeit verzehnfacht sich. Man kann beim Spazierengehen einen ganzen Feature-Branch durchcoden.

**Was es dafür braucht:**
- Claude Code mit Voice-Native-Interface (existiert in Beta)
- AI-Brille mit Heads-Up-Display für Code-Diffs
- Robuste Speech-to-Code-Pipeline (Whispr + Claude-Tooling)
- Disziplin: Voice-Coding funktioniert nur mit klaren Konventionen, sonst entsteht Chaos

### Szenario C · Design-Review im Spatial Mode

**Heute:** Joern öffnet Mockups in Browser, kommentiert via WhatsApp oder Chat-Tools.

**2026/27:** Joern setzt Vision-Pro/AR-Brille auf, das Cockpit-Mockup steht als 1:1-Mockup im Raum vor ihm. Er deutet auf die Burn-Run-Karte: *"Diese Farbe ist zu dunkel im Dark-Mode. Probier nochmal Coral 80%."* Das System:

- Erkennt durch Eye-Tracking + Hand-Pointing das gemeinte Element
- Modifiziert das Mockup live
- Speichert den Kommentar als Inline-Comment ins GitHub-PR
- Wenn Joern fertig ist, hat Claude Code automatisch einen PR mit allen Änderungen vorbereitet

**Konsequenz:** Design-Reviews werden **physisch und intuitiv** statt Screen-zu-Screen-Diktat. Joern und Max können in derselben virtuellen Session sein, beide deuten auf Elemente, sprechen drüber, ändern direkt. Das Mockup ist nicht mehr Bild — es ist Raum.

### Szenario D · Operations-Dashboard im Sichtfeld

**Heute:** Cockpit auf iPhone oder Desktop. Man muss aktiv reinschauen.

**2026/27:** Wichtige Live-Signale (Heute-Umsatz, kritische Standort-Issues, eingehende Voice-Calls) werden Max **passiv ins Sichtfeld** eingeblendet. Wie ein HUD im Auto. Er sagt *"Details Berlin Kreuzberg"* und das Standort-Detail klappt auf.

**Konsequenz:** Dashboards werden **ambient**. Man muss nicht reinschauen — die Information kommt zu einem, wenn sie wichtig ist.

---

## Teil 6 · Warum diese Zukunft kein Sci-Fi ist

Drei Gründe, warum das nicht in 10 Jahren, sondern in 12-24 Monaten Alltag wird:

1. **Die Hardware ist da:** Meta Ray-Ban Display (2025), Apple Vision Pro 2, AR-Brillen von Xreal, Brilliant Labs. Preise fallen rapide.
2. **Die AI ist da:** Claude 4+, GPT-5+, Native Voice-Modelle, Multimodale Eingabe. Speech-to-Action ist gelöstes Problem.
3. **Die Workflows sind da:** N8N, Odoo, GitHub-API, Tool-Use, Function-Calling. Wir müssen nicht erfinden — wir müssen verbinden.

Was BookaBox einzigartig macht: **Wir bauen kleine genug, um schnell umsteigen zu können, und groß genug, um den ROI zu rechtfertigen.** 100 Standorte mit klassischer Operations-Crew sind teuer. 100 Standorte mit Voice-First-Operations sind profitabel ab Standort 30.

---

## Teil 7 · Was die nächsten 16 Wochen passiert

**Wochen 1-4:** Knowledge-Repo `bookabox-knowledge` als zentraler Anker etabliert. Operating-System-Doc gepflegt. Erste Skills aus Drive in GitHub migriert.

**Wochen 5-8:** Cockpit-Redesign live. Mobile-First. Ask-AI integriert. 4 neue Standorte onboardet.

**Wochen 9-12:** N8N produktiv auf Hetzner. WhatsApp-Agent migriert. Quality-Agent geht in Beta — erste Standorte mit Live-Issue-Detection.

**Wochen 13-16:** Voice-First-Pilot. Eine Person (Max oder Jasmin) führt einen Quartal-Audit ausschließlich mit AI-Brille + Voice durch. Lernen, Iterieren. Falls erfolgreich: Rollout auf alle Audits.

---

## Teil 8 · Die zwei Sätze, die alles zusammenhalten

> **"Odoo speichert. N8N orchestriert. Claude denkt. Mensch entscheidet."**

> **"Wenn ein Workflow nicht über Voice geht, ist er noch nicht fertig designt."**

---

## Anhang · Glossar für Außenstehende

- **Cockpit:** Unsere interne Operations-Dashboard-Webapp. Heute Mobile-First-Redesign live.
- **GmbH:** Jeder BookaBox-Standort ist juristisch eine eigene GmbH. 100 Standorte = 100 GmbHs. Buchhaltungs-Komplexität ist real.
- **Move-out:** Kündigungs-Flow. Vom Kunden-Trigger bis zur sauberen, bereiten Box.
- **Skill (im Paperclip-Kontext):** Eine in Markdown geschriebene Anweisung an einen AI-Agenten — quasi ein Sub-Prompt mit klarem Trigger.
- **Knowledge-Repo:** Zentrales GitHub-Repo `bookabox-knowledge`, das alle Briefs, Specs, Brand-Guidelines hostet. Single Source of Truth für menschliches und maschinelles Lesen.
- **Voice-First:** Designprinzip, dass jeder Workflow primär per Sprache bedienbar sein soll, Tastatur als Fallback.

---

## Aufnahme-Hinweise für NotebookLM

- Tonalität: Nüchtern, gut informiert, fachlich präzise. Kein Marketing-Sprech.
- Wenn der Podcast in zwei Stimmen aufgenommen wird, soll eine die "fragende" Rolle spielen (Investor / Neuer Mitarbeiter), die andere die "erklärende" (Insider).
- Schwerpunkt im Audio: 30% heutiger Stack, 50% Zukunfts-Szenarien (besonders Voice + AI-Brille), 20% Strategie und Roadmap.
- Klingt am besten, wenn die Sprecher gelegentlich kontroverse Fragen einwerfen ("Ist das nicht zu früh?", "Wie willst du Privacy lösen, wenn ständig Kameras laufen?")

---

*Stand: Mai 2026 · Owner: Max · Living Document — wird quartalsweise aktualisiert.*
