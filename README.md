# n8n + Vapi Voice Agent

## Overview

This repository contains an n8n workflow for building an advanced AI voice agent using [Vapi.ai](https://vapi.ai/) as the voice platform and n8n as the automation backend.

Vapi manages the real-time voice interaction, while n8n handles tool calls (function calling) triggered by the voice agent. This allows the agent to perform actions like API calls, database operations, calendar bookings, and more during live conversations.

## Features

- Natural, real-time voice conversations (supports multiple languages and voices)
- Function tool integration: Vapi calls n8n webhooks to execute custom logic
- Easy customization: Update prompts, tools, and workflows in the dashboards
- Scalable: Handles inbound/outbound calls, web calls, or embedded voice
- Integrations: Google Calendar, Airtable, CRMs (e.g., GoHighLevel), APIs, and more via n8n nodes

## Prerequisites

- A [Vapi.ai](https://vapi.ai/) account (with credits for calls)
- An [n8n](https://n8n.io/) instance (self-hosted or cloud)
- Phone number (via Vapi, Twilio, or other provider) for inbound/outbound calls
- API keys/credentials for any external services (e.g., Google Calendar OAuth)

## Setup Instructions

### 1. Import the Workflow into n8n
- Copy the provided workflow JSON (from `workflow.json` or the template link).
- In n8n, create a new workflow → Import from clipboard/URL.
- Configure credentials (e.g., Google Calendar, HTTP auth if needed).

### 2. Activate Webhooks in n8n
- Open the Webhook node(s) in the workflow.
- Activate the workflow to generate production webhook URLs.
- Copy the production URL(s) – you'll need them in Vapi.

### 3. Configure the Assistant in Vapi
- Log in to your Vapi dashboard.
- Create a new Assistant (or edit an existing one).
- Set the system prompt (example provided below).
- Add **Function Tools**:
  - Name: Match exactly to your n8n tool logic (e.g., `checkAvailability`, `bookAppointment`).
  - Parameters: Define JSON schema for inputs.
  - Server URL: Paste the n8n production webhook URL.
- Assign a phone number or configure for web/outbound calls.
- Choose voice provider (e.g., ElevenLabs, Play.ht) and model (e.g., GPT-4o).

### 4. Test the Agent
- Call your Vapi phone number (or start a web session).
- Speak naturally – the agent will use tools via n8n as needed.
- Monitor logs in both Vapi and n8n dashboards for debugging.

### Example System Prompt (Paste into Vapi Assistant)
You are a helpful AI voice assistant [describe role, e.g., for scheduling appointments at a clinic].
Be friendly, concise, and natural in conversation.
When you need to perform an action (e.g., check availability or book a slot), use the provided tools.
Always confirm details with the user before finalizing.
text### Customization Tips
- Add more tools: Create additional webhooks in n8n and function tools in Vapi.
- Handle responses: In n8n, return JSON in Vapi's expected format `{ "result": "Your message to speak" }`.
- Error handling: Use n8n's error workflow or IF nodes.
- Memory/Persistence: Integrate with tools like Mem0 for conversation history across calls.

### Troubleshooting
- Tool not triggering? Ensure tool names match exactly and webhook is production (not test).
- No response from n8n? Check n8n logs and webhook accessibility (public URL required).
- Call quality issues? Adjust voice/model settings in Vapi.

### Resources
- Vapi Docs: https://docs.vapi.ai/
- n8n Workflow Templates: Search "Vapi" on https://n8n.io/workflows
- Example Tutorials: Search YouTube for "n8n Vapi integration"

Feel free to fork and adapt this for your use case!
