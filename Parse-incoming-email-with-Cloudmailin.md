* Generate a new UUID and copy it to your clipboard. Mac users, you can type `uuidgen | pbcopy` in your terminal to do this.
* Create a new Webhook agent, paste in the UUID as your secret and set the payload path to `.`
* In your new agent's summary, you'll see a URL like `https://YOUR_DOMAIN/users/1/web_requests/15/YOUR_SECRET`, copy that to your clipboard
* Sign up for an account on [Cloudmailin](https://www.cloudmailin.com)
* In the second step, you'll be prompted for a URL, paste in your webhook URL. For the format, select 'JSON Format'

You're done. Send an email to the new email address that you get from Cloudmailin, and you'll see an event. You can hook up other agents to your new agent to process these events further.