# 📞 AI Voice Calling Agent — Real Estate Automation

> **A 24/7 AI voice receptionist that answers property inquiries and books viewings automatically — built with Vapi, n8n, and OpenAI.**

`Vapi` · `n8n` · `OpenAI GPT-4.1-mini` · `Google Sheets` · `Google Calendar` · `WhatsApp Business API`

---

## 🧠 What Is This?

This project is a **fully automated AI voice calling agent** built specifically for real estate businesses. When a customer calls your number, an AI assistant named **Ben** picks up — instantly, every time, day or night. Ben understands what the caller is asking, looks up live property data, and books viewing appointments — all without any human involvement.

Think of it as hiring a receptionist who **never sleeps, never misses a call, never forgets a detail, and books every appointment in under 2 seconds.**

---

## ❌ The Problem It Solves

Real estate agents constantly face the same frustrations:

- 📵 **Missed calls = missed leads.** If no one picks up, the client moves on to the next agent.
- 🕐 **Availability limits.** Clients call evenings and weekends. You can't always be there.
- 📋 **Manual booking is slow.** Collecting name, email, phone, address, and preferred time — then entering it into a calendar — takes time and is error-prone.
- 💬 **You're handling admin, not sales.** Every minute spent answering basic property questions is a minute not spent closing deals.

This AI agent solves all four problems at once.

---

## ✅ What It Can Do

### 🔍 1. Instant Property Search
A caller asks: *"Can you tell me about the property at 123 Skyline Road?"*

Ben immediately queries your **live Google Sheets property database** and responds with full details — bedrooms, bathrooms, price, square footage, and description. No waiting. No hold music. No human needed.

> **What this means for you:** Your property database is always up to date (just edit the Sheet), and every caller gets accurate information instantly.

---

### 📅 2. Smart Viewing Bookings
A caller says: *"I'd like to book a viewing."*

Ben collects all required information through natural conversation:
- Full name
- Phone number
- Email address
- Property address
- Preferred date and time

Once confirmed, a **Google Calendar event is created automatically** — with the caller added as an attendee and all booking details included.

> **What this means for you:** Your calendar fills itself. You never have to manually enter a booking again.

---

### 📱 3. Real-Time Agent Notifications
The moment a viewing is booked, your **WhatsApp receives an instant notification** with the full booking summary — name, contact details, property, and confirmed time.

> **What this means for you:** You're always in the loop without being on the phone. Review bookings at a glance, on your phone, wherever you are.

---

## 🔄 How a Real Call Works

Here is a real example of what happens when a customer calls:

| Step | What Happens |
|------|-------------|
| **1. Customer calls** | The phone rings — Ben answers within 1 second |
| **2. Customer asks about a property** | *"Do you have anything at 123 Skyline Road?"* |
| **3. Ben triggers the backend** | Vapi sends the request to n8n via webhook |
| **4. AI Agent searches** | Queries Google Sheets for matching property |
| **5. Ben responds** | *"Yes! 4 bedrooms, 3 bathrooms, 2,200 sq ft, priced at $450,000 — with an attached garage and updated kitchen."* |
| **6. Customer wants a viewing** | *"I'd like to book a viewing."* |
| **7. Ben collects details** | Name → Phone → Email → Date & Time, one at a time |
| **8. Booking is confirmed** | Google Calendar event created, WhatsApp sent to agent |
| **9. Ben wraps up** | *"You're all set! Our agent will be in touch shortly."* |

The entire flow — from question to confirmed booking — happens in a single phone call, fully automated.

---

## 🏗️ System Architecture

```
[Customer Phone Call]
         │
         ▼
 [Vapi Voice AI — "Ben"]
  • Speech-to-text (Deepgram)
  • AI conversation (GPT-4o)
  • Text-to-speech (Elliot voice)
         │
         │  tool call (structured JSON)
         ▼
 [n8n Webhook — POST endpoint]
         │
         ▼
 [Extract Tool Args — Code Node]
  • Parses: toolCallId, Type, Name,
    Email, Phone, Viewing_Time, Address
         │
         ▼
 [AI Agent — OpenAI GPT-4.1-mini]
         │
         ├──► [Google Sheets Tool]
         │     → Reads live property database
         │     → Returns: beds, baths, price, sqft, description
         │
         ├──► [Google Calendar Tool]
         │     → Creates viewing appointment
         │     → Adds caller as attendee
         │     → Sets location to property address
         │
         └──► [WhatsApp Business API Tool]
               → Sends booking summary to agent
               → Includes all caller details
         │
         ▼
 [Respond to Webhook]
  • Returns: { results: [{ toolCallId, result }] }
         │
         ▼
 [Vapi receives the answer]
         │
         ▼
 [Ben speaks the response to the caller]
```

---

## 🛠️ Tech Stack

| Tool | Role | What It Does in This Project |
|------|------|-------------------------------|
| **Vapi** | Voice AI Platform | Handles inbound phone calls, speech recognition, and text-to-speech. The "face" of the agent. |
| **n8n** | Workflow Automation | The backend brain — orchestrates all logic, routing, and integrations. |
| **OpenAI GPT-4.1-mini** | Language Model | Powers the AI Agent's decision-making: decides whether to search, book, or notify. |
| **Google Sheets** | Property Database | Stores all property listings. Fully editable — update a cell and Ben immediately knows. |
| **Google Calendar** | Booking System | Auto-creates viewing events with attendee details and property location. |
| **WhatsApp Business API** | Agent Notifications | Sends instant booking alerts to the real estate agent's WhatsApp. |
| **Deepgram** | Speech Transcription | Converts caller voice to text with high accuracy (2.3% WER). |

---

## ⚡ Key Features

- ✅ **24/7 availability** — never misses a call, no matter the time or day
- ✅ **Human-like conversation** — natural voice (Elliot by Vapi), not a robotic IVR menu
- ✅ **Live property data** — reads directly from Google Sheets (no hardcoded info)
- ✅ **Automatic calendar booking** — creates full event with attendee invite
- ✅ **WhatsApp agent alert** — instant notification on every confirmed booking
- ✅ **Handles both query types in one call** — property info AND booking, seamlessly
- ✅ **Low cost** — approximately $0.11/min call cost
- ✅ **Fast** — under 2 seconds response time on every turn
- ✅ **Scalable** — add more properties to the Sheet; no code changes needed

---

## 📁 Project Files

```
Voice Calling Agent/
│
├── docs/
│   └── README.md            ← You are here
│
├── main-workflow.json        ← Complete n8n workflow (ready to import)
│
└── .agents/                 ← Claude Code AI development rules
    └── workflows/
        └── wf-1.md          ← Agent behavior guidelines
```

**The most important file is `main-workflow.json`** — it contains the entire backend workflow and can be imported directly into any n8n instance to get the system running.

---

## 🚀 How to Deploy This

Getting this live requires four steps:

1. **Import the workflow** — open n8n, go to Workflows → Import → upload `main-workflow.json`
2. **Connect credentials** — link your OpenAI API key, Google Sheets account, Google Calendar account, and WhatsApp Business API
3. **Update Vapi tool URL** — in Vapi's tool settings, point the server URL to your n8n production webhook:
   ```
   https://your-n8n-domain.com/webhook/bcb238ed-fc58-4303-8bd6-94366023f289
   ```
4. **Activate the workflow** — toggle it on in n8n → the agent is live

> No server setup required. n8n handles all hosting. The only external accounts needed are the four integrations listed above.

---

## 📦 Deliverables

Everything needed to run this system is included or documented:

| Deliverable | Status |
|-------------|--------|
| n8n workflow (importable JSON) | ✅ Included (`main-workflow.json`) |
| Vapi assistant configuration | ✅ Configured & tested |
| Google Sheets integration (live data) | ✅ Working |
| Google Calendar auto-booking | ✅ Working |
| WhatsApp agent notification | ✅ Working |
| Webhook → Vapi response loop | ✅ Fixed & verified |
| End-to-end testing | ✅ Completed (property search + full booking flow) |

---

## 💡 Who Is This For?

This system is ideal for any **real estate agency, property management company, or independent agent** who:

- Receives more calls than they can handle
- Loses leads because no one answers after hours
- Spends too much time on repetitive admin (answering the same property questions, manually booking appointments)
- Wants to look professional and tech-forward to clients
- Operates a small team without a dedicated receptionist

It can be adapted for **other industries too** — clinics, salons, dental offices, law firms, service businesses — anywhere appointment booking over the phone is a daily task.

---

## 📬 Contact

Built by **Harmain Rizwan** — AI Automation Developer specializing in voice agents, n8n workflows, and OpenAI integrations.

> Available for custom builds, modifications, and white-label deployments on [Upwork](https://www.upwork.com).
