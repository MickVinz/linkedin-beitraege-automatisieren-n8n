# LinkedIn Beiträge automatisieren (n8n Workflow)

Zwei n8n-Workflows, die wissenschaftliche Paper (PDF) oder spontane Sprachideen per Telegram in publikationsreife LinkedIn-Posts verwandeln – inklusive KI-Bildgenerierung mit Human-in-the-Loop-Freigabe und automatischer Veröffentlichung.

## Inhalt

- `CMS_Automatisierung (1).json` – n8n-Workflow: Telegram-Agent (PDF/Voice/Text) → Zusammenfassung, Übersetzung, LinkedIn-Post-Erstellung, Bildgenerierung mit Freigabe-Loop, Airtable-Ablage
- `LinkedinPost (1).json` – n8n-Workflow: Täglicher 8-Uhr-Trigger, veröffentlicht offene Entwürfe aus Airtable automatisch auf LinkedIn
- `Social-Media-Automatisierung_mit_KI.png` – Infografik zum Workflow
- `Screenshot 2026-07-17 133039.png` – Screenshot
- `einleitung.txt` – Begleitartikel mit allen Takeaways

## Übersicht

![Workflow-Übersicht](Social-Media-Automatisierung_mit_KI.png)

## Screenshots

![Screenshot](Screenshot%202026-07-17%20133039.png)

## Setup

1. `CMS_Automatisierung (1).json` und `LinkedinPost (1).json` in n8n importieren
2. Credentials verknüpfen: Telegram Bot, OpenAI (GPT-4o Mini, DALL-E 3, Transkription), Airtable, Google Drive, LinkedIn
3. Airtable-Base mit Feldern Titel, Zusammenfassung, Status, Bild anlegen
4. Schedule Trigger (8:00 Uhr) für `LinkedinPost` aktivieren

## Funktionsweise

1. **Telegram-Agent**: Nimmt PDF, Sprachmemo oder Text entgegen, erkennt Trigger-Wörter, verwaltet Einträge per Get-Record-ID-Tool
2. **PDF-Pipeline (Basic LLM Chains)**: Titel-Übersetzung → Zusammenfassung → LinkedIn-Post (max. 150 Wörter, Plain Text) → Quellenangabe im AMA-Format
3. **Bildgenerierung mit Freigabe**: DALL-E-3-Bild wird in Telegram gepostet, per Approve/Decline-Button freigegeben, danach Upload zu Google Drive
4. **Veröffentlichung**: Separater Workflow prüft täglich um 8:00 Uhr Airtable auf offene Entwürfe, postet sie via LinkedIn API und setzt Status auf „Erledigt“

## Tech Stack

- **n8n** – Orchestrator
- **Airtable** – Content-Datenbank (Status-Workflow, Kanban/Kalender-Views)
- **Telegram** – Steuerung & Voice-Interface
- **Google Drive** – Medienspeicher
- **OpenAI (GPT-4o Mini & DALL-E 3)** – Text- und Bildgenerierung
