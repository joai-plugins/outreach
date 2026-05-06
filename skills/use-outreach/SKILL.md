---
name: use-outreach
description: Use the Outreach JoAi app plugin when the task needs Outreach tools or workflows.
---

# Outreach

Connect Outreach to Claude, Codex, and ChatGPT through JoAi's hosted MCP app server.

If a specific task was given, identify the relevant MCP tool and call it immediately — no preamble.

If invoked with no task, call the authenticate tool first (if present), then list the available actions concisely so the user can pick one.

Never ask "what would you like to do?" — either act on the task or show the menu.

## Example Prompts

- List the Outreach tools available in this app.
- Explain what setup or authentication Outreach needs before I run an action.
- Use Outreach to help me with the task I describe next.

## Action Inventory

- `outreach-ai-draft` (collect, prompt) — Draft a personalized outreach message for a contact. Fetches the contact's profile and recent activity history, then uses AI to write a context-aware message tailored to the chosen occasion. Returns the draft for human review — does not send.
- `outreach-broadcast` (collect) — Compose and send a message to all contacts in a segment or tag.
- `outreach-contact-message` (collect, collect, prompt, collect) — Send a personalized outreach message to a specific CRM contact.
- `outreach-dashboard` (collect, collect, collect, collect) — View and manage your outreach pipeline. See enrolled contacts, their current sequence step, parked contacts, and reply status in one overview.
- `outreach-enroll` (collect, collect, collect) — Enroll a CRM contact into an outreach sequence by setting the sequence name and resetting their step to 1. The host system schedules execution of the first template.
- `outreach-execute-step` (collect, collect, prompt, collect, collect) — Execute one step of an outreach sequence for a contact: fetch the contact and matching template, personalize the message, send or log it depending on channel, then advance the contact to the next step.
- `outreach-handle-reply` (collect, collect) — Record that a contact replied to an outreach message. Tags the contact as 'outreach-replied' so the sequence can be stopped and the response handled manually or by the agent.
- `outreach-log-touch` (collect) — Record a single outreach interaction (WhatsApp, email, LinkedIn, post, call) on a CRM contact with structured meta so A/B tests and funnel analytics stay trackable.
- `outreach-park` (collect) — Mark an outreach contact as parked, pausing their sequence. Useful when a contact needs a break from automated touches or when manual follow-up is needed.
- `outreach-score-update` (collect, prompt, collect) — Compute a 0-100 engagement score for a contact based on the recency, frequency, and variety of interactions in their timeline, and store it on the contact as the engagement_score property. Lets agents and operators surface relationships that are weakening over time.
- `outreach-segment-scan` (collect, prompt) — Identify contacts in a segment or tag that are ready for proactive outreach.
- `outreach-stats` (collect) — Return outreach touches filtered by template, variant, channel and date range. Powers reply-rate and A/B comparison views.
- ...and 1 more actions exposed by the hosted MCP app server.

## Usage Notes

- Every listed action becomes an MCP tool when the app server is connected.
- Prefer the generated provider plugin when one is available, and fall back to the raw MCP URL otherwise.

## Auth Notes

- Some actions require provider credentials or OAuth on first use.
