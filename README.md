# Build Then Break: n8n Templates

Free workflows from the Build Then Break YouTube channel (https://www.youtube.com/@BuildThenBreak).
Every workflow here was built on camera, broken on purpose, and fixed. The fixes are included.

## Watch order

New to n8n? Watch in this order. The "Files" column names the section below that holds that video's workflows (section numbers follow the order the templates were added, not the channel's video numbers).

| # | Video | Files |
|---|---|---|
| **Start here** | | |
| 1 | [What Is an AI Agent? I Built One. Then It Lied.](https://youtu.be/YVyHxnFd6wA) | Video 3 |
| 2 | [AI Sorts My Leads in n8n. Then It Broke 3 Times](https://youtu.be/lPwNu1Exbzg) | Video 1 |
| **Production n8n** ([playlist](https://www.youtube.com/playlist?list=PLBD87MjyasF4)) | | |
| 3 | [Part 1: Self-Host n8n for Free on Your PC (Docker)](https://youtu.be/IEDtvkKk4ZE) | Video 4 |
| 4 | [Part 2: n8n Error Handling: My Workflow Failed Silently](https://youtu.be/KVdqqi4dNNw) | Video 9 |
| 5 | [Part 3: I Let AI Run My Business Inbox for 10 Days](https://youtu.be/iInk9oEfvDQ) | Video 8 |
| 6 | Part 4: n8n Gmail Trigger Not Working: 5 Reasons Emails Get Skipped | Video 13 |
| **Builds** | | |
| 7 | [AI Email Assistant in n8n: Reads Gmail, Drafts Replies](https://youtu.be/WfiweQKkm-Q) | Video 6 |
| 8 | [Chat With Your PDFs in n8n for Free. Then It Lied.](https://youtu.be/7I0xNO_W7Dc) | Video 5 |
| 9 | [n8n AI Agent Books Meetings From Chat. It Picked 2023.](https://youtu.be/Sqivae3DsP0) | Video 7 |
| 10 | [5 n8n Automations for a Small Business (All Free)](https://youtu.be/OtWQ7PEnjMQ) | Video 10 |
| 11 | [n8n WhatsApp AI Chatbot. Then It Forgot the Order](https://youtu.be/V70092dao-M) | Video 12 |
| **Comparisons** | | |
| 12 | [Zapier vs Make vs n8n: Same AI Workflow, All 3 Broke](https://youtu.be/vMKm-ZAVdYg) | Video 2 |
| 13 | [4 Free AIs Built My Bakery a Website. I Tested Them](https://youtu.be/V0x1Y1chHB0) | Video 11 |

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

## Video 4: Self-Host n8n for Free on Your PC
- No workflow file. This video is the Docker setup only. The one command and the fixes are in the video description: https://youtu.be/IEDtvkKk4ZE

## Video 5: Chat With Your PDFs (RAG)
- `video5-chat-with-pdf-rag.json`: upload side (form, Simple Vector Store, Gemini embeddings) and chat side (AI Agent, retrieve tools). Test PDFs: `Bright_Dental_Patient_Handbook.pdf`, `Sunrise_Dental_Patient_Guide.pdf`, `Supplier_Price_Sheet.pdf` (contains a prompt-injection line on purpose).
- Needs a Gemini key for embeddings and chat. The Simple Vector Store is in-memory; it resets on restart.

## Video 6: AI Email Assistant
- `video6-ai-email-assistant.json`: Gmail trigger, AI text classifier (lead, support, newsletter, other), labels, draft replies (never sends), AI Processed label, mark as read. Set your own sender filter in the Gmail trigger.

## Video 7: AI Calendar Booking Agent
- `video7-ai-calendar-booking-agent.json`: chat trigger, AI Agent, check_availability, create_event, list_events, with the date/time and booking rules in the system message. Needs a Google Calendar OAuth credential and a Gemini key.

## Video 8: I Let AI Run My Business Inbox for 10 Days
- The experiment ran the Video 6 workflow (`video6-ai-email-assistant.json`) on a real inbox with the sender filter removed. 64 emails arrived, 49 were sorted, 15 were never touched.
- `video8-ai-email-assistant-with-fixes.json`: the same assistant with the fixes from the video. Retry On Fail (3 tries, 5 seconds apart) on the classifier and the draft writer, and an "Own alert?" check before the classifier so emails with "failed" in the subject, or from your alerts address, go straight to Needs Review. Set your alerts address in that node and pick your labels in the four label nodes.
- `video8-daily-missed-email-check.json`: every morning at 9, searches `in:inbox -label:ai-processed newer_than:1d` and emails you the list (or "nothing skipped"). Keep it as a separate workflow so it still runs when the assistant is down. Set your own email in the last node.
- For red runs, add the Video 9 error workflow (`video9-error-alerting.json`) as the Error Workflow in the assistant's settings.

## Video 9: n8n Error Handling
- `video9-error-alerting.json`: Error Trigger, Gmail alert, Alert Log sheet as a backup when the email fails. Set it as the Error Workflow in any workflow's settings.
- `video1-lead-sorter-with-error-logging.json`: the lead sorter with "continue using error output", an "AI FAILED - check manually" row, and the trimmed If condition.
- Import steps: add a second tab called `Alert Log` to your leads sheet with the columns in `video9-alert-log-headers.csv` (Time, Workflow, Error); import both JSONs; add credentials (Gmail, Google Sheets, Gemini); pick your sheet in the three Sheets nodes and set your own email in the Gmail node; publish the alert workflow; in the lead sorter open Settings > Error Workflow and pick it.

## Video 10: 5 Free Automations for a Small Business
- `video10-demo1-lead-auto-reply.json`: contact form, spam filter ("Skip spam"), sheet row, instant reply. Replace `YOUR_GOOGLE_SHEET_ID` with your own sheet.
- `video10-demo2-invoice-to-sheet.json`: invoice PDF upload, Gemini Analyze Document, sheet row. Test files: `Invoice_Northwind_Supplies.pdf` (text) and `Invoice_Riverside_SCANNED.pdf` (scanned).
- `video10-demo3-weekly-report.json`: Monday schedule, read Sales tab, AI summary, email. "Always Output Data" is on so empty weeks still send a report.

## Video 11: I Asked 4 Free AIs to Build a Business Website
- No n8n workflow. The four websites exactly as each AI built them (after the Round 2 to 4 changes and the Formspree fix):
  - `video11-bakery-site-chatgpt.html`
  - `video11-bakery-site-claude.html`
  - `video11-bakery-site-gemini.html`
  - `video11-bakery-site-kimi.html`
- To try one: save it as `index.html` in its own folder and drag the folder onto Netlify Drop. Replace `YOUR_FORM_ID` with your own Formspree form ID to make the contact form deliver. Gemini's version never got the Formspree link (that is the point of the video). Kimi's "Pay by card" is a demo and takes no payment: do not put it online for a real business.
- Live copies: https://maple-chatgpt.netlify.app · https://maple-claude.netlify.app · https://maple-gemini.netlify.app · https://maple-kimi.netlify.app

## Video 12: WhatsApp AI Chatbot (Burger Hub, fast food demo)
- `video12-whatsapp-restaurant-bot.json`: WhatsApp Trigger (On messages) > "Has message?" (stops Meta's sent / delivered / read status updates) > "Is text?" > AI Agent with Gemini and Simple Memory (one conversation per phone number) > WhatsApp reply. Voice notes, photos and anything that isn't text get a fixed "please type your order" reply instead of silence.
- Credentials: a WhatsApp OAuth credential for the trigger (Meta App ID + App Secret), a WhatsApp API credential for the two reply nodes (a System User token that never expires, not the 24-hour token from the setup page, plus your WhatsApp Business Account ID), and a Gemini key.
- After import: set `YOUR_PHONE_NUMBER_ID` in both reply nodes (Meta > WhatsApp > API Setup), and change the menu in the AI Agent's system message.
- n8n on your own PC: Meta can't reach `localhost`. Run a tunnel (for example `cloudflared tunnel --url http://localhost:5678`) and start n8n with `WEBHOOK_URL` set to the tunnel address. A free quick tunnel gets a new address on every restart, so use a named tunnel or a server for a real business.
- Meta checklist: publish the app (needs a privacy policy URL) and subscribe your WhatsApp Business Account to the app (`POST /{WABA_ID}/subscribed_apps` in the Graph API Explorer), or real messages never reach n8n.
- Simple Memory is wiped when n8n restarts. For a real restaurant, use a database memory (for example Postgres).

## Video 13: n8n Gmail Trigger Not Working, 5 Reasons Emails Get Skipped
- `video13-gmail-trigger-5-fixes.json`: the two-step test from the video (Gmail Trigger every minute > Gmail "Add label" `Seen by n8n`), with all five fixes already in. If an email gets the label, n8n saw it.
- The 5 reasons, as tested on n8n 2.42: (1) the workflow was saved but never **published**; (2) **Read status: unread only** and the email was read while n8n was off, so it is never picked up; (3) a change was **saved but not published again**, so the old version kept running; (4) the trigger was limited to the **INBOX** label and a Gmail filter skipped the inbox; (5) **Execute Once** on the next step, so of 3 emails in one poll only the first was handled.
- Setup: create a Gmail label called `Seen by n8n`, connect your Gmail credential on both nodes, pick the label in the second node, publish, send yourself a test email.
- Good news: the trigger remembers its last check, so emails that arrive while n8n is down are picked up after a restart (up to "Max Emails per Poll" per minute), as long as they are still unread or you use "Unread and read".
- Also check: if your Gmail credential uses your own Google Cloud OAuth app in "Testing" mode, Google expires the connection after 7 days. Set the app to "In production".
- Safety net: the daily missed-email check from Video 8 (`video8-daily-missed-email-check.json`) finds anything that slipped through.
