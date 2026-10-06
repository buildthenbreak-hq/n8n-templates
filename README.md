# Build Then Break: n8n Templates

Free workflows from the Build Then Break YouTube channel (https://www.youtube.com/@BuildThenBreak).

## Workflows
- Video 1: n8n contact form AI classifier (Form > OpenAI > Google Sheets > Gmail)
  Video 1 needs a Google Sheet with these columns: Name, Email, Message, Category, Received_at (see video1-leads-sheet-headers.csv).
- Video 2: Lead Router (Google Sheets trigger > Gemini > Sheets update > If > Gmail), the n8n build from "Zapier vs Make vs n8n"
- Video 3: AI agent lead assistant (Chat trigger > AI Agent with memory, Google Sheets tool and Gmail tool), from "What Is an AI Agent?"

## How to import
1. Download the .json file.
2. In n8n, open Workflows > Import from File.
3. Add your own credentials (Google Sheets, Gmail, Gemini or OpenAI).
4. Replace the prompt or sheet with your own.

## Video 3: import steps
1. Create a Google Sheet and import video3-agent-leads.csv.
2. In n8n: Workflows > Import from File > video3-ai-agent-lead-assistant.json.
3. Add your own credentials: OpenAI (or another chat model), Google Sheets, Gmail.
4. In the Google Sheets tool, pick your sheet. In the Gmail tool, set your own email in To.
5. Open the chat and ask: How many sales leads do we have?
