**Warning: ** This feature is still in development.

To use the new Services integration you first need to set up OAuth applications for the external services you would like to use.

## Twitter

If you don't have a Twitter Application yet, please visit the following URL: https://apps.twitter.com

You'll need to name your application.  Perhaps something like: `John's Huginn`
You'll also need a description, which could be: `John's personal Huginn system (http://github.com/cantino/huginn)`.
The required website could be your personal site, or your Twitter profile URL.

The Callback URL is important, you need to set it to the following: `http://<your-huginn-domain.com>/auth/twitter/callback`, replace `<your-huginn-domain.com>` with your domain name. 

On the "API Keys" page you need your "API Key" and "API Secret". Open your Huginn `.env` file and set `TWITTER_OAUTH_KEY` to the `API Key` and `TWITTER_OAUTH_SECRET` to the `API Secret`.

After your restarted your Huginn instance you should be able to authenticate with Twitter via the Services page.

## 37signals (Basecamp)

If you do not have a 37signals Application yet, visit https://integrate.37signals.com/ and create a new one.

Choose a name for your application, enter your company's name (or your own) and enter a website URL (can be anything).

In the "Integration" section you need to enable "Basecamp", the other 37signals applications are optional.

In the "Redirect URI" text field enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/37signals/callback`

After you created your application you should see your "Client ID" and "Client Secret". Open your Huginn `.env` file and set `37SIGNALS_OAUTH_KEY` to the `Client ID` and `37SIGNALS_OAUTH_SECRET` to the `Client Secret`.

After your restarted your Huginn instance you should be able to authenticate with 37signals via the Services page.