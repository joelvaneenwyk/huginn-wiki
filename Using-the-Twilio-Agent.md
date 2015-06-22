The Twilio Agent, as the name implies, allows arbitrary agent networks to output events to [Twilio](https://www.twilio.com/).  Unless you've written code specific to Twilio in the past trying to use this agent effectively can be a somewhat daunting task.  This wiki page aims to resolve that.

To access your Twilio account, you need to set up a TwiML app for your account on this page: [https://www.twilio.com/user/account/apps](https://www.twilio.com/user/account/apps).  You can call it whatever you want ('Huginn' works).  Each TwiML app requires that two Request URLs be configured, one for voice and one for SMS and MMS.  Both of these can be the front page of your Huginn instance (https://huginn.example.com/).  If you are running in DEVELOPMENT mode and have set up HTTP Basic Auth in front of your instance, it is recommended that you set up a second account specifically used to permit Twilio access.  The URL would then look something like this: https://twilio:password@huginn.example.com/).

Twilio Agent can accept as its input the keys {{message}}, {{text}}, or {{sms}} and are Liquid enabled.  The values of these keys cannot exceed 160 characters in length.

Twilio Agent requires a phone number to contact: {{receiver_cell}}

The configuration keys {{receive_text}} and {{receive_call}} are somewhat misleading in how they are named.  They are Boolean switches which determine whether the phone number specified in {{receiver_cell}} will receive a text message, a phone call (the message will be run through a speech synthesis system at Twilio), or both.  At least one must be set to 'true' for this agent to do anything.

If you don't have a paid Twilio account all messages sent through this service will have a standard "Buy a real account" nag prepended.