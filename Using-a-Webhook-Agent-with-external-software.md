At its most basic, the [Webhook Agent](https://github.com/cantino/huginn/blob/master/app/models/agents/webhook_agent.rb) presents a way to get arbitrary data into Huginn for processing.  Every time data is POSTed to a Webhook Agent, one or more events are created and emitted to downstream Huginn agents.  Think of Webhook Agent like a general purpose REST API endpoint, the mechanics of which are defined by whatever contacts the endpoint.  To put it another way, POST a JSON document to the Webhook Agent, and do whatever you want with the keys and values inside of Huginn.

A few things to remember about the Webhook Agent:
* Webhook Agent URLs look like this: **https://huginn.example.com/users/1/web_requests/948/neverGonnaGiveYouUp**
* The **/users/1/** part of the Huginn URI represents the Huginn user in question.  **/users/1/** is the user 'admin' (or whatever you've renamed 'admin' to), **/users/2/** would be the second user created, and so on.
* The **/web_requests/** part of the Huginn URI can be interpreted to mean "REST API rail for Webhook Agents."
* **/948/** refers to the Huginn agent ID number (in this case, agent #948).  This number will be different for every instance of the Webhook Agent.
* Every instance of Webhook Agent has a configuration field called _secret_, which is basically an API key to authenticate whatever contacts it from the outside.  This really should be different for every Webhook Agent to minimize potential impact of it being compromised, and should be treated like a password.  (See also <a href="https://github.com/cantino/huginn/issues/1070">ticket #1070</a>.)
* If you have a web server in front of Huginn acting as a reverse proxy and implementing HTTP auth, **and** your Webhook Agent needs to be accessible from the public Net, you'll have to set up an HTTP auth account which can be used to log in from outside (see also <a href="https://github.com/cantino/huginn/issues/815">ticket #815</a>).  Then your URLs will look like this: **https://webhookuser@webhookpassword:huginn.example.com/users/1/web_requests/948/neverGonnaLetYouDown**
* You can also write code which runs on the same host as Huginn and not have to worry about HTTP auth: **http://localhost:3000/users/1/web_requests/948/neverGonnaRunAroundAndDesertYou**

Webhook Agent currently supports the following HTTP methods:
* POST (the default)
* GET

Information POSTed into a Webhook Agent must be correctly formatted JSON.  All HTTP requests made to a Webhook Agent must have the **Content-Type: application/json** HTTP header, otherwise you'll get bizarre results.

Usage Example:

Assume for the moment that you're writing [Python code which interfaces with a Webhook Agent](https://github.com/virtadpt/exocortex-halo/tree/master/web_search_bot).  An array of URLs called **search_results** will be POSTed to the Webhook Agent:

    search_results = ["https://www.example.com/", "http://site.example.com"]

The **Content-Type** header is implemented with a dictionary:

    custom_headers = { "Content-Type": "application/json" }

The POST request could be programmed and executed this way (using the [Requests module](http://docs.python-requests.org/en/latest/) for clarity):

    results = { "results": search_results }
    request = requests.post(webhook, data=json.dumps(results), headers=custom_headers)