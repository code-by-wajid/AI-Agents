# Class 7 - Building a Scalable AI Receptionist with N8N



## Lesson Overview

This lesson covers building a complete, production-ready **receptionist agent** that can handle real customer interactions, manage bookings, and integrate with business tools.

The example built is for a restaurant, but the same agent architecture works for salons, clinics, law firms, gyms — any business that takes appointments. Only the system prompt and a few Google Sheet columns need to change; the workflow, tools, and logic stay identical. This means the same agent can be deployed for any client in any industry with minimal modification.

## What I Learned

- How to structure a production-grade AI agent workflow
- Building booking management (create, modify, cancel appointments)
- Integrating with Google Sheets for a booking database
- Connecting Google Calendar for automatic scheduling
- Sending confirmation emails via Gmail
- Handling edge cases and error scenarios
- How to adapt this agent for different industries in under 10 minutes
- Testing and debugging the agent for reliability

## My Build: Restaurant Receptionist Workflow

Built an n8n workflow named **"Receptionist"** — an AI agent that acts as a restaurant's booking assistant. Structure of the workflow:

- **Trigger:** "When chat message received" — starts the conversation
- **AI Agent (core node):** receives the chat input and orchestrates all connected components
- **Chat Model:** OpenAI Chat Model powers the agent's reasoning and responses
- **Memory:** Simple Memory — lets the agent retain context across the conversation
- **Tools connected to the AI Agent:**
  - **Google Sheets** — Append row, Delete rows or columns, Update row (used as the booking database — creating, modifying, and canceling reservations)
  - **Google Calendar** — Create event, Delete event, Get many events (used for automatic scheduling and checking availability)
  - **Gmail** — Send a message (used for sending booking confirmation emails)

This mirrors the production pattern from the lesson: one AI Agent node orchestrating multiple tools (Sheets + Calendar + Gmail), all driven by a single system prompt that defines the agent's role as a restaurant receptionist. Adapting this for another business type (e.g. a clinic or salon) would mean updating the system prompt and the sheet's column structure — the rest of the workflow stays the same.

## Key Takeaway

A single, well-structured agent + tool-set pattern is reusable across industries. The "intelligence" of adapting to a new business lives in the **system prompt and data structure**, not in rebuilding the workflow logic from scratch — this is what makes agents like this scalable for real client work.

---

*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*