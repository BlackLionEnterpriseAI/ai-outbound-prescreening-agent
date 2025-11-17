# SMS Setup (Make.com + Twilio Example)

1. Create a Twilio account and buy a phone number.
2. In Make.com, add the Twilio module:
   - "Send an SMS"
3. Map:
   - To: Phone column from your sheet
   - Body: AI-generated sms_body
4. Set up a webhook in Twilio for incoming SMS to connect back to Make.com for handling replies.
