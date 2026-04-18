# Alice — AI Personal Assistant for Institutional Finance

> **Production n8n agentic workflow powering a Telegram-based AI chief-of-staff — built for institutional allocators managing complex deal flow, diligence pipelines, and investor relationships.**

[![n8n](https://img.shields.io/badge/n8n-workflow-FF6D5A?style=flat)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/GPT--4.1-powered-412991?style=flat&logo=openai&logoColor=white)](https://openai.com/)
[![Pinecone](https://img.shields.io/badge/Pinecone-RAG-blue?style=flat)](https://pinecone.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## What Is This?

Alice is a production AI agent deployed as a personal Telegram assistant for institutional investment professionals. It handles multi-modal inputs (text, voice, and images), routes them through a specialized AI agent, and executes real actions across Gmail, Google Calendar, Notion, and a proprietary Pinecone knowledge base.

Built on a finance-specific system prompt encoding 20+ years of institutional due diligence expertise, Scout functions as an intelligent chief-of-staff — triaging inbound deal flow, prepping for manager meetings, drafting communications, and maintaining institutional memory.

---

## Architecture

```
Telegram (text / voice / photo)
          │
          ▼
    ┌─────────────┐
    │   Switch    │  ← routes by input type
    └──┬──┬──┬───┘
       │  │  │
  Text │  │  │ Photo
       │  │  └──► GPT-4o Vision → Extract content
       │  │
       │  └──► Whisper → Transcribe audio
       │
       ▼
┌─────────────────────────────────────┐
│           Scout AI Agent            │
│         (GPT-4.1 + Tools)           │
│                                     │
│  Tools:                             │
│  ├── Gmail (send/reply/draft/label) │
│  ├── Google Calendar (CRUD)         │
│  ├── Notion CRM                     │
│  ├── Notion Idea Hopper             │
│  ├── Notion Sales Pipeline          │
│  ├── Pinecone RAG (knowledge base)  │
│  ├── Tavily Web Search              │
│  ├── Google Sheets (contacts)       │
│  └── Window Buffer Memory           │
└──────────────┬──────────────────────┘
               │
               ▼
         Telegram reply
```

---

## Agent Capabilities

### Due Diligence & Research
- Analyze fund managers, PPMs, DDQs, and term sheets
- Query proprietary Pinecone knowledge base for historical manager data
- Web search via Tavily for real-time intelligence
- Meeting prep: brief on investors and generate key diligence questions

### Email Management
- Send, reply, draft, and label emails via Gmail
- HTML-formatted drafts — always saves as draft, never auto-sends
- Retrieve and triage inbound messages

### Calendar Management
- Create, update, delete, and query Google Calendar events
- Schedule meetings with attendees

### CRM & Pipeline
- Query and update Notion CRM contacts
- Log ideas to Notion Idea Hopper
- Track and update Notion Sales Pipeline

### Multi-Modal Input
- **Text** — direct command processing
- **Voice** — Whisper transcription → agent
- **Image** — GPT-4o vision extraction → agent

---

## Agent System Prompt

Scout is configured as an institutional finance executive assistant with deep domain expertise:

- Uses hedge fund terminology correctly (NAV, DDQ, PPM, side letters, drawdown)
- Checks CRM before responding to questions about any person or company
- Routes "idea" keywords automatically to Notion Idea Hopper
- Concise Telegram-optimized responses (2-4 sentences unless detailed analysis requested)
- Never fabricates — if information isn't in the knowledge base, says so explicitly

---

## Prerequisites

- [n8n](https://n8n.io/) (self-hosted or cloud)
- Telegram Bot (via BotFather)
- OpenAI API key (GPT-4.1 + Whisper + Embeddings)
- Pinecone account + index
- Google OAuth (Gmail + Calendar + Sheets)
- Notion API key + database IDs
- Tavily API key

---

## Setup

1. Import `Altbots_Personal_AI_sanitized.json` into your n8n instance
2. Configure credentials for each service (see Prerequisites)
3. Update the following placeholders in the workflow:
   - `YOUR_CALENDAR_ID` → your Google Calendar ID
   - `YOUR_SHEET_ID` → your contacts Google Sheet ID
   - `YOUR_NOTION_DB_ID` → your Notion database IDs
   - `YOUR_TAVILY_API_KEY` → your Tavily API key
4. Update the Scout system prompt with your own context
5. Activate the workflow
6. Message your Telegram bot to test

---

## Related Projects

| Project | Description |
|---------|-------------|
| [altbots-tearsheet](https://github.com/NeilD-NYC/altbots-tearsheet) | AI pipeline generating institutional manager tearsheets |
| [demo-altbots-io](https://github.com/NeilD-NYC/demo-altbots-io) | Portfolio intelligence dashboard |
| [AltBots Platform](https://altbots.io) | Full institutional research platform |

---

## Background

**Neil Datta** — Founder, AltBots / NKD Advisory LLC

Former MD & Global Head of Risk & Diligence at Optima/Forbes Family Trust ($24B MFO). 2,000+ manager reviews. 500+ investments closed. $9B+ deployed across alternative asset classes. Building AI infrastructure for institutional finance since 2022.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-in%2Fneildatta-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/neildatta)

---

## License

MIT — see [LICENSE](./LICENSE)
