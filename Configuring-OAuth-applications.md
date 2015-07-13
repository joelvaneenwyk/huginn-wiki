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

* If you're hosting Huginn yourself, open your Huginn `.env` file and set `THIRTY_SEVEN_SIGNALS_OAUTH_KEY` to the `Client ID` and `THIRTY_SEVEN_SIGNALS_OAUTH_SECRET` to the `Client Secret`.
* If you're using Heroku, set the necessary environment variables with `heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
* If you're using OpenShift, set the necessary environment variables with `rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with 37signals via the Services page.


## Wunderlist

If you do not have a Wunderlist Application yet, visit https://developer.wunderlist.com/applications and click 'Create new Application'.

You need to choose a name for your application and an App URL (can be your huginn instance or anything else).

In the "Authorization Callback URL" field you need to enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/wunderlist/callback`

After you create your application you should see your "Client ID" and "Client Secret". As with Twitter above, do the following:

* If you're hosting Huginn yourself, open your Huginn `.env` file and set `WUNDERLIST_OAUTH_KEY` to the `Client ID` and `WUNDERLIST_OAUTH_SECRET` to the `Client Secret`.
* If you're using Heroku, set the necessary environment variables with `heroku config:set WUNDERLIST_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set WUNDERLIST_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
* If you're using OpenShift, set the necessary environment variables with `rhc env set WUNDERLIST_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set WUNDERLIST_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with Wunderlist via the Services page.

## Dropbox

If you do not have a Dropbox Application yet, visit https://www.dropbox.com/developers/apps/create, select dropbox API app, let it access all the folders, all file types, and click 'Create app'.

You need to choose a name for your application and an App URL (can be your huginn instance or anything else).

In the "Redirect URIs" field you need to enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/dropbox/callback`

After you create your application you should see your "Client ID" and "Client Secret". As with Twitter above, do the following:

* If you're hosting Huginn yourself, open your Huginn `.env` file and set `DROPBOX_OAUTH_KEY` to the `Client ID` and `DROPBOX_OAUTH_SECRET` to the `Client Secret`.
* If you're using Heroku, set the necessary environment variables with `heroku config:set DROPBOX_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set DROPBOX_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
* If you're using OpenShift, set the necessary environment variables with `rhc env set DROPBOX_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set DROPBOX_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with Dropbox via the Services page.

# Debugging Twitter

## Twitter error: Invalid Status code 420

You may get 420 errors when you use the same Twitter credentials locally and in production, or if you're accidentally running multiple instances of the threaded worker, or perhaps if the threaded worker did not shut down properly (again causing many copies to be running).