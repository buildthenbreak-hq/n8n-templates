# Build Then Break: n8n Templates

Free workflows from the Build Then Break YouTube channel (https://www.youtube.com/@BuildThenBreak).
Every workflow here was built on camera, broken on purpose, and fixed. The fixes are included.

## How to import
1. Download the .json file.
2. In n8n, open Workflows > Import from File.
3. Add your own credentials (Google Sheets, Gmail, Google Calendar, Gemini or OpenAI).
4. Replace the prompt, sheet or email with your own.

## Video 1: AI Lead Sorter
- `video1-contact-form-ai-classifier.json`: contact form, AI classifier, Google Sheets, Gmail. Needs a sheet with columns Name, Email, Message, Category, Received_at (see `video1-leads-sheet-headers.csv`).

## Video 2: Lead Router (from "Zapier vs Make vs n8n")
- `video2-lead-router-gemini.json`: Google Sheets trigger, Gemini, Sheets update, If, Gmail. Needs the same sheet columns as Video 1.

## Video 3: AI Agent Lead Assistant (from "What Is an AI Agent?")
- `video3-ai-agent-lead-assistant.json`: chat trigger, AI Agent with memory, Google Sheets tool and Gmail tool.
- Import steps: create a Google Sheet and import `video3-agent-leads.csv`; import the JSON; add credentials (chat model, Google Sheets, Gmail); pick your sheet in the Sheets tool and set your own email in the Gmail tool; open the chat and ask "How many sales leads do we have?"

## Video 5: Chat With Your PDFs (RAG)
- `video5-chat-with-pdf-rag.json`: upload side (form, Simple Vector Store, Gemini embeddings) and chat side (AI Agent, retrieve tools). Test PDFs: `Bright_Dental_Patient_Handbook.pdf`, `Sunrise_Dental_Patient_Guide.pdf`, `Supplier_Price_Sheet.pdf` (contains a prompt-injection line on purpose).
- Needs a Gemini key for embeddings and chat. The Simple Vector Store is in-memory; it resets on restart.

## Video 6: AI Email Assistant
- `video6-ai-email-assistant.json`: Gmail trigger, AI text classifier (lead, support, newsletter, other), labels, draft replies (never sends), AI Processed label, mark as read. Set your own sender filter in the Gmail trigger.

## Video 7: AI Calendar Booking Agent
- `video7-ai-calendar-booking-agent.json`: chat trigger, AI Agent, check_availability, create_event, list_events, with the date/time and booking rules in the system message. Needs a Google Calendar OAuth credential and a Gemini key.

## Video 9: n8n Error Handling
- `video9-error-alerting.json`: Error Trigger, Gmail alert, Alert Log sheet as a backup when the email fails. Set it as the Error Workflow in any workflow's settings.
- `video1-lead-sorter-with-error-logging.json`: the lead sorter with "continue using error output", an "AI FAILED - check manually" row, and the trimmed If condition.

## Video 10: 5 Free Automations for a Small Business
- `video10-demo1-lead-auto-reply.json`: contact form, sheet row, instant reply.
- `video10-demo2-invoice-to-sheet.json`: invoice PDF upload, Gemini Analyze Document, sheet row. Test files: `Invoice_Northwind_Supplies.pdf` (text) and `Invoice_Riverside_SCANNED.pdf` (scanned).
- `video10-demo3-weekly-report.json`: Monday schedule, read Sales tab, AI summary, email. "Always Output Data" is on so empty weeks still send a report.
