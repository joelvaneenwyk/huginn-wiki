To use the new Services integration you first need to set up OAuth applications for the external services you would like to use.

## Twitter

If you don't have a Twitter Application yet, please visit the following URL: https://apps.twitter.com

You'll need to name your application.  Perhaps something like: `John's Huginn`
You'll also need a description, which could be: `John's personal Huginn system (http://github.com/cantino/huginn)`.
The required website could be your personal site, or your Twitter profile URL.

The Callback URL is important, you need to set it to the following: `http://<your-huginn-domain.com>/auth/twitter/callback`, replace `<your-huginn-domain.com>` with your domain name. 

On the "API Keys" page you need to note down your "API Key" and "API Secret", and then:

* If you're hosting Huginn yourself, open your Huginn `.env` file and set `TWITTER_OAUTH_KEY` to the `API Key` and `TWITTER_OAUTH_SECRET` to the `API Secret`.
* If you're using Heroku, set the necessary environment variables with `heroku config:set TWITTER_OAUTH_KEY=YOUR-KEY` and `heroku config:set TWITTER_OAUTH_SECRET=YOUR-SECRET`.
* If you're using OpenShift, set the necessary environment variables with `rhc env set TWITTER_OAUTH_KEY=YOUR-KEY` and `rhc env set TWITTER_OAUTH_SECRET=YOUR-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with Twitter via the Services page.

## 37signals (Basecamp)

If you do not have a 37signals Application yet, visit https://integrate.37signals.com/ and create a new one.

Choose a name for your application, enter your company's name (or your own) and enter a website URL (can be anything).

In the "Integration" section you need to enable "Basecamp", the other 37signals applications are optional.

In the "Redirect URI" text field enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/37signals/callback`

After you create your application you should see your "Client ID" and "Client Secret". As with Twitter above, do the following:

* If you're hosting Huginn yourself, open your Huginn `.env` file and set `37SIGNALS_OAUTH_KEY` to the `Client ID` and `37SIGNALS_OAUTH_SECRET` to the `Client Secret`.
* If you're using Heroku, set the necessary environment variables with `heroku config:set 37SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set 37SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
* If you're using OpenShift, set the necessary environment variables with `rhc env set 37SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set 37SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with 37signals via the Services page.