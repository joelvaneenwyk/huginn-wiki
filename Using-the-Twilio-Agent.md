The Twilio Agent, as the name implies, allows arbitrary agent networks to output events to [Twilio](https://www.twilio.com/). If you haven't previously written code specific to Twilio, using this agent effectively can be somewhat daunting. This wiki page aims to resolve that.

## Setting Up Your Twilio Account

To access your Twilio account, you need to set up a TwiML app. Follow these steps:
1. Go to the [Twilio Apps Page](https://www.twilio.com/user/account/apps).
2. Create a new TwiML app (you can name it 'Huginn' or any other name you prefer).
3. Each TwiML app requires two Request URLs to be configured: one for voice and one for SMS/MMS. Both of these URLs should point to the front page of your Huginn instance, e.g., https://huginn.example.com/.
4. If you are running in DEVELOPMENT mode and have set up HTTP Basic Auth for your instance, it is recommended to set up a second account specifically for Twilio access. The URL would then look something like this: https://twilio:password@huginn.example.com/.

## Configuring the Twilio Agent

The Twilio Agent can accept the following keys as its input: {{message}}, {{text}}, or {{sms}}. These keys are Liquid enabled. Please note that the values of these keys cannot exceed 160 characters in length.

### Required Configuration
* Phone Number: The agent requires a phone number to contact, specified by the key {{receiver_cell}}.

### Optional Configuration
* Receive Text ({{receive_text}}): A Boolean switch that determines if the specified phone number will receive a text message.

* Receive Call ({{receive_call}}): A Boolean switch that determines if the specified phone number will receive a phone call (the message will be run through Twilio's speech synthesis system).

At least one of {{receive_text}} or {{receive_call}} must be set to true for the agent to function.

### Notes
* If you don't have a paid Twilio account, all messages sent through this service will have a standard "Buy a real account" nag prepended.