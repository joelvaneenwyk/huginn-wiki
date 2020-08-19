**Problem**: Certain sites have ugly source code and/or render the page using JavaScript, making it next to impossible to use the Website Agent. (Described in issue [#888](https://github.com/cantino/huginn/issues/888))

**Solution**: Use [browserless](https://www.browserless.io/) to emulate the browser and return a fully rendered DOM. This allows the Website Agent to then properly scrape dynamic content from JavaScript-heavy pages.

In order to use *browserless*, deploy an own instance first. See https://github.com/browserless/chrome for more installation instructions (Docker image available at https://hub.docker.com/r/browserless/chrome).

In Huginn, the **Post Agent** will request the rendered html from *browserless* for a given url through an API call (https://docs.browserless.io/docs/content.html). These are the values to set in the **Post Agent**
* `post_url` - set to *browserless_url/content* (where *browserless_url* is wherever the instance is hosted)
* `content_type` - usually set to *json*
* `method` - set to *post*
* `payload` - set to `{url: site_url}` where *site_url* is the url of the site that should be rendered
* `emit_events` - set to *true* (this will allow setting this agent as the source for the html of the desired site)

The remaining keys can stay at their default values.

Try a dry run to confirm that the agent returns rendered html.

**Website Agent** - *WIP*