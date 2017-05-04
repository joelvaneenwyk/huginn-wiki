## CSV Agent
The `CsvAgent` parses or serializes CSV data. When parsing, events can either be emitted for the entire CSV, or one per row.
Set `mode` to `parse` to parse CSV from incoming event, when set to `serialize` the agent serilizes the data of events to CSV.


## Webhook Agent
The Webhook Agent will create events by receiving webhooks from any source. In order to create events with this agent, make a POST request to:

`https://localhost:3000/users/1/web_requests/:id/:secret`

The placeholder symbols above will be replaced by their values once the agent is saved.


## Tumblr Likes Agent
The Tumblr Likes Agent checks for liked Tumblr posts from a specific blog.
To be able to use this Agent you need to authenticate with Tumblr in the Services section first.


## Twilio agent
The Tumblr Likes Agent checks for liked Tumblr posts from a specific blog.
To be able to use this Agent you need to authenticate with Tumblr in the Services section first.


## Javascript Agent
The JavaScript Agent allows you to write code in JavaScript that can create and receive events. If other Agents aren’t meeting your needs, try this one!


## Dropbox Watch Agent
The Dropbox Watch Agent watches the given dir_to_watch and emits events with the detected changes.


## Aftership Agent
The Aftership agent allows you to track your shipment from aftership and emit them into events.
To be able to use the Aftership API, you need to generate an `API Key`. You need a paying plan to use their tracking feature.
You can use this agent to retrieve tracking data.


## Manual Event Agent
The Manual Event Agent is used to manually create Events for testing or other purposes.
Do not set options for this Agent. Instead, connect it to other Agents and create Events using the UI provided on this Agent’s Summary page.


## Telegram Agent
The Telegram Agent receives and collects events and sends them via Telegram.


## Attribute Difference Agent
The Attribute Difference Agent receives events and emits a new event with the difference or change of a specific attribute in comparison to the previous event received.


## JSON Parse Agent
The JSON Parse Agent parses a JSON string and emits the data in a new event
`data` is the JSON to parse. Use Liquid templating to specify the JSON string.
`data_key` sets the key which contains the parsed JSON data in emitted events


## Jabber Agent
The Jabber Agent will send any events it receives to your Jabber/XMPP IM account.


## De Duplicate Agent
The De-duplication Agent receives a stream of events and remits the event if it is not a duplicate.


## Google Translation Agent
The Translation Agent will attempt to translate text between natural languages.
Services are provided using Google Translate. You can sign up to get `google_api_key` which is required to use this agent. The service is **not free**.


## Data output Agent
The Data Output Agent outputs received events as either RSS or JSON. Use it to output a public or private stream of Huginn data.


## Adioso Agent
The Data Output Agent outputs received events as either RSS or JSON. Use it to output a public or private stream of Huginn data.


## Email Digest Agent
The Email Digest Agent collects any Events sent to it and sends them all via email when scheduled. The number of used events also relies on the `Keep events` option of the emitting Agent, meaning that if events expire before this agent is scheduled to run, they will not appear in the email.


## The Tumblr Publish Agent 
The Tumble Publish Agent publishes Tumblr posts from the events it receives.
To be able to use this Agent you need to authenticate with Tumblr in the Services section first.


## Weibo User Agent
The Weibo User Agent follows the timeline of a specified Weibo user. It uses this endpoint: `http://open.weibo.com/wiki/2/statuses/user_timeline/en`


## Pushover Agent
The Pushover Agent receives and collects events and sends them via push notification to a user/group.


## S3 Agent
The S3Agent can watch a bucket for changes or emit an event for every file in that bucket. When receiving events, it writes the data into a file on S3.


## Post Agent
A Post Agent receives events from other agents (or runs periodically), merges those events with the Liquid-interpolated contents of `payload`, and sends the results as POST (or GET) requests to a specified url. To skip merging in the incoming event, but still send the interpolated payload, set `no_merge` to `true`.


## Twitter Action Agent
The Twitter Action Agent is able to retweet or favorite tweets from the events it receives.


## Twitter Favourites
The Twitter Favorites List Agent follows the favorites list of a specified Twitter user.


## Twitter User Agent
The Twitter User Agent either follows the timeline of a specific Twitter user or follows your own home timeline including both your tweets and tweets from people whom you are following.


## Twitter Search Agent
The Twitter Search Agent performs and emits the results of a specified Twitter search.


## Twitter Stream Agent
The Twitter Stream Agent follows the Twitter stream in real time, watching for certain keywords, or filters, that you provide.


## Twitter Publish Agent
The Twitter Publish Agent publishes tweets from the events it receives.


## Delay Agent
The DelayAgent stores received Events and emits copies of them on a schedule. Use this as a buffer or queue of Events.


## RSS Agent
The RSS Agent consumes RSS feeds and emits events when they change.
This agent, using Feedjira as a base, can parse various types of RSS and Atom feeds and has some special handlers for FeedBurner, iTunes RSS, and so on. However, supported fields are limited by its general and abstract nature. For complex feeds with additional field types, we recommend using a WebsiteAgent. 


## Google Calendar Agent
The Google Calendar Publish Agent creates events on your Google Calendar.
This agent relies on service accounts, rather than oauth.


## Local File Agent
The LocalFileAgent can watch a file/directory for changes or emit an event for every file in that directory. When receiving an event it writes the received data into a file.
mode determines if the agent is emitting events for (changed) files or writing received event data to disk.


## User Location Agent
The User Location Agent creates events based on WebHook POSTS that contain a `latitude` and `longitude`. You can use the POSTLocation or PostGPS iOS app to post your location to `https://localhost:3000/users/1/update_location/:secret` where `:secret` is specified in your options.


## Wunderlist Agent
The WunderlistAgent creates new Wunderlist tasks based on the incoming event.


## Weibo Publish Agent
The Weibo Publish Agent publishes tweets from the events it receives.
You must first set up a Weibo app and generate an access_token for the user that will be used for posting status updates.


## Growl Agent
The Growl Agent sends any events it receives to a Growl GNTP server immediately.
It is assumed that events have a message or text key, which will hold the body of the growl notification, and a subject key, which will have the headline of the Growl notification. You can use Event Formatting Agent if your event does not provide these keys.


## IMAP Folder Agent
The Imap Folder Agent checks an IMAP server in specified folders and creates Events based on new mails found since the last run. In the first visit to a folder, this agent only checks for the initial status and does not create events.


## Evernote Agent
The Evernote Agent connects with a user’s Evernote note store.
Visit Evernote to set up an Evernote app and receive an api key and secret. Store these in the Evernote environment variables in the .env file. You will also need to create a Sandbox account to use during development.


## Twilio Receive Agent
The Twilio Receive Text Agent receives text messages from Twilio and emits them as events.
In order to create events with this agent, configure Twilio to send POST requests to:

`https://localhost:3000/users/1/web_requests/:id/sms-endpoint`

The placeholder symbols above will be replaced by their values once the agent is saved.


## Hipchat Agent
The Hipchat Agent sends messages to a Hipchat Room


## Commander Agent
The Commander Agent is triggered by schedule or an incoming event, and commands other agents (“targets”) to run, disable, configure, or enable themselves.


## Peak Detector Agent
The Peak Detector Agent will watch for peaks in an event stream. When a peak is detected, the resulting Event will have a payload message of `message`.


## Dropbox File URL Agent
The DropboxFileUrlAgent is used to work with Dropbox. It takes a file path (or multiple files paths) and emits events with either temporary links or permanent links.


## Liquid Output Agent
The Liquid Output Agent outputs events through a Liquid template you provide. Use it to create a HTML page, or a json feed, or anything else that can be rendered as a string from your stream of Huginn data.


## Read File Agent
The ReadFileAgent takes events from `FileHandling` agents, reads the file, and emits the contents as a string.


## Change Detector Agent
The Change Detector Agent receives a stream of events and emits a new event when a property of the received event changes.

## Witai Agent
The `wit.ai` agent receives events, sends a text query to your `wit.ai` instance and generates outcome events.


## Public Transport Agent
The Public Transport Request Agent generates Events based on NextBus GPS transit predictions.


## Shell Command Agent
The Shell Command Agent will execute commands on your local system, returning the output.


## Phantom JS Cloud Agent
This Agent generates PhantomJs Cloud URLs that can be used to render JavaScript-heavy webpages for content extraction.

URLs generated by this Agent are formulated in accordance with the PhantomJs Cloud API. The generated URLs can then be supplied to a Website Agent to fetch and parse the content.
Sign up to get an api key, and add it in Huginn credentials.


## Digest Agent
The Digest Agent collects any Events sent to it and emits them as a single event.
The resulting Event will have a payload message of `message`. You can use liquid templating in the `message`, have a look at the Wiki for details.


## PDF Info Agent
The PDF Info Agent returns the metadata contained within a given PDF file, using HyPDF.


## Human Task Agent
The Human Task Agent is used to create Human Intelligence Tasks (HITs) on Mechanical Turk.
HITs can be created in response to events, or on a schedule. Set trigger_on to either schedule or event.


## Stubhub Agent
The StubHub Agent creates an event for a given StubHub Event.
It can be used to track how many tickets are available for the event and the minimum and maximum price. All that is required is that you paste in the url from the actual event, e.g. `https://www.stubhub.com/outside-lands-music-festival-tickets/outside-lands-music-festival-3-day-pass-san-francisco-golden-gate-park-polo-fields-8-8-2014-9020701/`


## Website Agent
The Website Agent scrapes a website, XML document, or JSON feed and creates Events based on the results.


## Sentiment Agent
The Sentiment Agent generates `good-bad` (psychological valence or happiness index), `active-passive` (arousal), and `strong-weak` (dominance) score. It will output a value between 1 and 9. It will only work on English content.


## Gap Detector Agent
The Gap Detector Agent will watch for holes or gaps in a stream of incoming Events and generate “no data alerts”.


## Email Agent
The Email Agent sends any events it receives via email immediately.
You can specify the email’s subject line by providing a subject option, which can contain Liquid formatting. E.g., you could provide "Huginn email" to set a simple subject, or {{subject}} to use the subject key from the incoming Event.
By default, the email body will contain an optional headline, followed by a listing of the Events’ keys.


## Boxcar Agent
The Boxcar agent sends push notifications to iPhone.
To be able to use the Boxcar end-user API, you need your `Access Token`. The access token is available on general “Settings” screen of Boxcar iOS app or from Boxcar Web Inbox settings page.


## FTPSite Agent
The Ftp Site Agent checks an FTP site and creates Events based on newly uploaded files in a directory. When receiving events it creates files on the configured FTP server.
`mode` must be present and either `read` or `write`, in `read` mode the agent checks the FTP site for changed files, with `write` it writes received events to a file on the server.


## Scheduler Agent
The Scheduler Agent periodically takes an action on target Agents according to a user-defined schedule.


## Pushbullet Agent
The Pushbullet agent sends pushes to a pushbullet device
To authenticate you need to either the `api_key` or create a `pushbullet_api_key` credential, you can find yours at your account page:
`https://www.pushbullet.com/account`


## Trigger Agent
The Trigger Agent will watch for a specific value in an Event payload.
The rules array contains hashes of `path`, `value`, and `type`. The `path` value is a dotted path through a hash in JSONPaths syntax. For simple events, this is usually just the name of the field you want, like ‘text’ for the text key of the event.


## Jira Agent
The Jira Agent subscribes to Jira issue updates.


## Event Formatting Agent
The Event Formatting Agent allows you to format incoming Events, adding new fields as needed.


## MQTT Agent
The MQTT Agent allows both publication and subscription to an MQTT topic.
MQTT is a generic transport protocol for machine to machine communication.


## HTTP Status Agent
The HttpStatusAgent will check a url and emit the resulting HTTP status code with the time that it waited for a reply. Additionally, it will optionally emit the value of one or more specified headers.


## Basecamp Agent
The Basecamp Agent checks a Basecamp project for new Events
To be able to use this Agent you need to authenticate with 37signals in the Services section first.


## Weather Agent
The Weather Agent creates an event for the day’s weather at a given `location`.


## Slack Agent
The Slack Agent lets you receive events and send notifications to Slack.

## Google Flights Agent
The GoogleFlightsAgent will tell you the minimum airline prices between a pair of cities.

