To use the new Services integration you first need to set up OAuth applications for the external services you would like to use.

## Twitter

If you don't have a Twitter Application yet, please visit the following URL: https://developer.twitter.com/en/apps

You'll need to name your application. Perhaps something like: `Johns Huginn` (requires an alphanumeric name)
You'll also need a description, which could be: `John's personal Huginn system (http://github.com/cantino/huginn)`.
The required website could be your personal site, or your Twitter profile URL.

The Callback URL is important, you need to set it to the following: `http://<your-huginn-domain.com>/auth/twitter/callback`, replace `<your-huginn-domain.com>` with your domain name.

On the "API Keys" page you need to note down your "API Key" and "API Secret", and then:

- If you're hosting Huginn yourself, open your Huginn `.env` file and set `TWITTER_OAUTH_KEY` to the `API Key` and `TWITTER_OAUTH_SECRET` to the `API Secret`.
- If you're using a Docker container use `HUGINN_TWITTER_OAUTH_KEY` for the `API Key` and `HUGINN_TWITTER_OAUTH_SECRET` for the `API Secret`. [More environment variables here.](https://hub.docker.com/r/cantino/huginn/)
- If you're using Heroku, set the necessary environment variables with `heroku config:set TWITTER_OAUTH_KEY=YOUR-KEY` and `heroku config:set TWITTER_OAUTH_SECRET=YOUR-SECRET`.
- If you're using OpenShift, set the necessary environment variables with `rhc env set TWITTER_OAUTH_KEY=YOUR-KEY` and `rhc env set TWITTER_OAUTH_SECRET=YOUR-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with Twitter via the Services page.

If you're having issues, see the [debugging section](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications#debugging-twitter) below.

## 37signals (Basecamp)

If you do not have a 37signals Application yet, visit https://integrate.37signals.com/ and create a new one.

Choose a name for your application, enter your company's name (or your own) and enter a website URL (can be anything).

In the "Integration" section you need to enable "Basecamp", the other 37signals applications are optional.

In the "Redirect URI" text field enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/37signals/callback`

After you create your application you should see your "Client ID" and "Client Secret". As with Twitter above, do the following:

- If you're hosting Huginn yourself, open your Huginn `.env` file and set `THIRTY_SEVEN_SIGNALS_OAUTH_KEY` to the `Client ID` and `THIRTY_SEVEN_SIGNALS_OAUTH_SECRET` to the `Client Secret`.
- If you're using Heroku, set the necessary environment variables with `heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
- If you're using OpenShift, set the necessary environment variables with `rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with 37signals via the Services page.

## Dropbox

If you do not have a Dropbox Application yet, visit https://www.dropbox.com/developers/apps/create, select dropbox API app, let it access all the folders, all file types, and click 'Create app'.

You need to choose a name for your application and an App URL (can be your huginn instance or anything else).

In the "Redirect URIs" field you need to enter the following and replace `<your-huginn-domain.com>` with the domain of your huginn instance `http://<your-huginn-domain.com>/auth/dropbox/callback`

After you create your application you should see your "Client ID" and "Client Secret". As with Twitter above, do the following:

- If you're hosting Huginn yourself, open your Huginn `.env` file and set `DROPBOX_OAUTH_KEY` to the `Client ID` and `DROPBOX_OAUTH_SECRET` to the `Client Secret`.
- If you're using Heroku, set the necessary environment variables with `heroku config:set DROPBOX_OAUTH_KEY=YOUR-CLIENT-ID` and `heroku config:set DROPBOX_OAUTH_SECRET=YOUR-CLIENT-SECRET`.
- If you're using OpenShift, set the necessary environment variables with `rhc env set DROPBOX_OAUTH_KEY=YOUR-CLIENT-ID` and `rhc env set DROPBOX_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

After your restarted your Huginn instance you should be able to authenticate with Dropbox via the Services page.

## Tumblr

To enable Tumblr integration you'll need to install the OAuth key and secret in the huginn/.env file. To acquire the OAuth keys isn't self-evident, so here's an attempt at documenting the process.

First, if you have Huginn behind a web server like Apache or Nginx with HTTP basic auth restricting access (and you should), you must use the htpasswd utility to create a username and password to provide access to the callback URLs: `sudo htpasswd -m /path/to/.htpasswd callback`

Log into your Tumblr dashboard and access your account settings. Click on "Apps". Scroll to the bottom of the page and click the Register link (https://www.tumblr.com/oauth/apps). Click the "+ Register application" button.

Enter the name for the application registration ("Huginn" works). Enter a description for your application; this can be freeform but please be descriptive so that Tumblr's owners don't decide to unilaterally ban Huginn from their service. The Default Callback URL is the problem because it's not documented in Huginn anywhere. It's supposed to look like this: `https://huginn.example.com/auth/tumblr/callback`

However, due to the fact that you have HTTP basic auth in front of Huginn you'll need to supply the username and password so that their OAuth implementation can reach the callback URL. Put this into the Default Callback URL field: `callback:password@https://huginn.example.com/auth/tumblr/callback`

If you feel like it, upload an icon and an application page icon for your Huginn integration. Solve the CAPTCHA. Click the Register button. You will be presented with your OAuth key and secret. Edit your huginn/.env file and plug these values into the `TUMBLR_OAUTH_KEY` and `TUMBLR_OAUTH_SECRET` fields, then restart Huginn.

Log into Huginn normally and click on Services. Click the "Authenticate with Tumblr" button and follow the prompts. You'll be returned to Huginn's services page and when you instantiate a Tumblr Publish Agent you will see that the Service field will be populated, and you will be able to configure it normally.

I recommend opening [Tumblr's API documentation](https://www.tumblr.com/docs/en/api/v2#posting) in another tab to assist in configuring the Tumblr Publish Agent. By default, every possible configuration option is present in a new Tumblr Publish Agent. There are several kinds of posts that can be made on Tumblr but not all of them require the same options; the presence of some options may cause the Agent to not save properly. So, delete the configuration options that are unnecessary; when in doubt, go with the bare minimum.

# Debugging OAuth Applications

## Debugging Twitter

### Twitter error: Invalid Status code 420

You may get 420 errors when you use the same Twitter credentials locally and in production, or if you're accidentally running multiple instances of the threaded worker, or perhaps if the threaded worker did not shut down properly (again causing many copies to be running).
