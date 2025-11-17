# Make.com Scenario – Outreach & Pre-Screening (Outline)

## Scenario 1: Initial Outreach (Email + SMS)

1. Trigger:
   - Manual (Run once) or Scheduled (e.g., every hour)
2. Module: Google Sheets / Excel
   - "Search Rows" or "List Rows" from your leads sheet
3. Module: Iterator
   - Iterate through each row (each lead)
4. Module: OpenAI / HTTP
   - Send lead data + templates to AI to generate personalized:
     - email_subject
     - email_body
     - sms_body
5. Module: Email (Gmail / SMTP / SendGrid)
   - Send email to `email` column using AI-generated subject/body
6. Module: SMS (Twilio / other)
   - Send SMS to `phone` column using AI-generated sms_body
7. Module: Google Sheets / CRM
   - Update row with:
     - date_outreach_sent
     - channel_used
     - outreach_status = "Sent"

## Scenario 2: Pre-Screening Responses

You’ll build one scenario per channel:

### A. Email Replies
1. Trigger: New email in Gmail with specific label (e.g., "Outreach Reply")
2. Module: OpenAI
   - Analyze reply → extract:
     - interest level (high/medium/low)
     - answers to pre-screen questions (if present)
3. Module: Google Sheets / CRM
   - Update the lead record with the extracted info

### B. SMS Replies
1. Trigger: Incoming SMS via Twilio webhook
2. Module: Router:
   - If reply is "YES" → send first pre-screening question
   - If reply contains an answer → store and send next question
3. Repeat until all 3 questions answered
4. Store responses in Google Sheets / CRM

> Note: LinkedIn/Instagram DMs require compliant tools or official APIs.
> Use providers that respect platform terms and avoid spam behavior.
