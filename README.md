# kalpi-assingment: n8n AI Support Automation

AI-powered customer support workflow (form intake -> AI response -> email reply) packaged for quick client setup.

---

## Quick start (TL;DR)
1) Install and start Docker Desktop.
2) In this folder, load the image and start the stack:
   ```bash
   docker load -i n8n-client.tar
   docker compose up -d
   ```
3) Open http://localhost:5678 and complete credential hookups (Google Sheets, Gmail, Gemini).

---

## What is included
- Prebuilt n8n image (`n8n-client.tar`) and `docker-compose.yml`.
- Ready-made **Form-Trigger-Agent** workflow for Google Form -> Sheets -> Gemini -> Gmail.

## Prerequisites
- Docker Desktop running.
- Google Cloud project with **Gmail API** and **Google Sheets API** enabled.
- OAuth client for Gmail and Google Sheets (client ID/secret) and account access to the target Sheet/Form.
- Gemini API key.

---

## Step-by-step setup
### 1) Install Docker
- Install Docker Desktop and ensure it is running before continuing.

### 2) Place the deployment folder
- Keep both files in the same directory: `n8n-client.tar`, `docker-compose.yml`.

### 3) Start the automation system
- In a terminal from this folder, run:
  ```bash
  docker load -i n8n-client.tar
  docker compose up -d
  ```
- Wait for containers to finish starting.

### 4) Open the n8n dashboard
- Visit http://localhost:5678.
- Confirm the **Form-Trigger-Agent** workflow is present.

### 5) Enable Google APIs
- In Google Cloud Console, enable **Google Sheets API** and **Gmail API**.
- Create OAuth credentials (client ID and secret).
- In n8n, add credentials for **Google Sheets** and **Gmail** using that OAuth client.

### 6) Create the Google Form
Fields to include:
- Full Name
- Email Address
- Query Category (options: Technical Support/Bug Report, Billing/Payment Inquiry, Product Information/Feature Request, General Feedback, Other)
- Describe Your Query in Detail

### 7) Connect the Form to Google Sheets
- Use the Sheet automatically created by the Form.
- In n8n, open the workflow and point the **Google Sheets Trigger** node to that Sheet.

### 8) Add the Gemini API key
- Obtain a Gemini API key.
- In n8n, add it under the **Gemini Chat Model** credential.

### 9) Activate the workflow
- Open the workflow and click **Activate**.
- The system will ingest form submissions, generate AI responses, send emails, and handle replies.

### 10) Test the system
- Submit a test entry through the Google Form.
- Confirm the workflow ingests the submission, produces a response, and sends the email.

---

## Credential checklist (you provide)
- Gmail OAuth (client ID/secret + consented account).
- Google Sheets OAuth (same project is fine).
- Gemini API key.

---

## Operate and stop
- View dashboard: http://localhost:5678
- Stop stack: `docker compose down`
- Restart after credential changes: `docker compose down && docker compose up -d`
