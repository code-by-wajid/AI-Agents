# Class 6 - Building AI Agents That Take Action



## Lesson Overview

This lesson goes beyond agents that just chat — it covers how AI agents actually **take action**: sending emails, creating calendar events, and interacting with external systems.

**Core idea:** Tools are the agent's "hands." Without tools, an agent can only talk. With tools, it can take real actions in the real world.

## What This Lesson Covers

- What tools are and why an agent needs them
- How AI agents decide *when* to call a tool
- How to structure effective system prompts for tool-using agents
- Understanding **tool anatomy**: credentials, resources, operations, parameters
- How to connect **Gmail** so an agent can send emails
- How to connect **Google Calendar** so an agent can book appointments
- Making API calls through tools

## Key Concept: Tool Anatomy

Every tool an agent uses is generally made up of:

- **Credentials** — the authentication/connection info needed to access the external service (e.g. Gmail login/API key)
- **Resources** — the type of "thing" being worked with (e.g. an email, a calendar event, a contact)
- **Operations** — the action to perform on that resource (e.g. send, create, update, delete)
- **Parameters** — the specific details/values needed to perform the operation (e.g. recipient, subject, body for an email)



*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*