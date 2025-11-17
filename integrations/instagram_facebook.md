# Instagram & Facebook Integration (ManyChat + Make.com)

## Goal
Use Instagram & Facebook as **engagement channels**:
- Auto-reply to DMs
- Start conversations from comments/keywords
- Pre-screen leads once they message us

We do NOT use IG/FB for mass cold spam. All automation must follow Meta’s policies.

---

## Architecture

User → IG/FB Page/Account → ManyChat → Make.com → AI → ManyChat → User

---

## Step 1 – Connect IG/FB to ManyChat

1. Create a ManyChat account.
2. Connect:
   - Instagram Business Account
   - Facebook Page
3. Turn on:
   - “Instagram DM Automation”
   - “Facebook Inbox Automation”

Now ManyChat can receive:
- New DMs
- Replies to stories
- Comment keyword triggers

---

## Step 2 – Create Entry Triggers

Examples:
- “When user sends a DM”
- “When user comments ‘AI’ on a post”
- “When user replies to a Story”

These triggers start a flow where we:
- Greet the user
- Ask permission or context
- Then hand off to the AI

---

## Step 3 – Connect to Make.com via Webhook

1. In Make.com:
   - Create a new Scenario.
   - Add first module: **Custom Webhook**.
2. Copy the webhook URL.
3. In ManyChat:
   - Add an action: “External Request” or “Send to Webhook”.
   - Paste the Make.com Webhook URL.
   - Send:
     - user_id
     - username / IG handle
     - their message
     - any tags you want

---

## Step 4 – Use AI in Make.com

1. After the Webhook module:
   - Add a module: OpenAI (or HTTP → OpenAI API).
2. Send:
   - system_prompt from `prompts/system_prompt.txt`
   - user’s message
   - any context (e.g. niche, offer)
3. Receive AI’s reply.

---

## Step 5 – Send Response Back to ManyChat

1. In Make.com:
   - Add an HTTP module to call back to ManyChat’s “Send Message” API endpoint.
   - Use the `user_id` from the initial webhook.
   - Send the AI-generated response.

2. In ManyChat:
   - The user receives the message as a DM.

---

## Compliance Notes

- Let users opt out (“Reply STOP to end messages” style).
- Do not send mass unsolicited DMs.
- Only trigger flows from user actions (DMs, comments, etc.).
