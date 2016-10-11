# Agent Configuration Examples

## WebsiteAgents

### Reddit Gold

Generate events whenever a comment receives gold on a specified subreddit. Here r/all is demonstrated.

    {
      "expected_update_period_in_days": 2,
      "url": "http://www.reddit.com/r/all/comments/gilded.json",
      "type": "json",
      "mode": "on_change",
      "extract": {
        "body": { "path": "$.data.children[*].data.body" },
        "title": { "path": "$.data.children[*].data.link_title" }
      }
    }

### Follow public posts on Google+

This can follow public posts of any page/person on Google+. An API key will be needed. In this example we are following +google.

    {
      "expected_update_period_in_days": 2,
      "url": "https://www.googleapis.com/plus/v1/people/+google/activities/public?key=<api-key>",
      "type": "json",
      "mode": "on_change",
      "extract": {
        "status": { "path": "$.items[*].object.content" },
        "title": { "path": "$.items[*].title" }
      }
    }

### Follow stock prices

This can follow stock prices. Here we are showing Google and Apple. Replace with any other companies to get their stock updates.


    {
      "expected_update_period_in_days": "2",
      "url" : "http://finance.yahoo.com/webservice/v1/symbols/GOOG,AAPL/quote?format=json",
      "type": "json",
      "mode": "all",
      "extract":  {
                     "name"  : {"path": "$.list.resources[*].resource.fields.name"},
                     "symbol": {"path": "$.list.resources[*].resource.fields.symbol"},
                     "price" : {"path": "$.list.resources[*].resource.fields.price"}
                   }
    }

### iTunes Trailers

This Agent follows iTunes trailers from the apple.com/trailers RSS feed.

    {
      "url": "http://trailers.apple.com/trailers/home/rss/newtrailers.rss",
      "mode": "on_change",
      "type": "xml",
      "expected_update_period_in_days": "10",
      "extract": {
        "title": {
          "css": "item title",
          "value": ".//text()"
        },
        "url": {
          "css": "item link",
          "value": ".//text()"
        }
      }
    }

### Bitcoin Rates

A Website Agent to collect Bitcoin rates.

    {
      "expected_update_period_in_days": "2",
      "url": "http://api.bitcoincharts.com/v1/weighted_prices.json",
      "type": "json",
      "mode": "on_change",
      "extract": {
        "24h": {
          "path": ".USD.24h"
        },
        "7d": {
          "path": ".USD.7d"
        },
        "30d": {
          "path": ".USD.30d"
        }
      }
    }

### Bitcoin Blockchain Watch.

A Website Agent to collect current blockchain height and timestamp.

    {
      "expected_update_period_in_days": "2",
      "url": "https://blockchain.info/latestblock",
      "type": "json",
      "mode": "on_change",
      "extract": {
        "height": {
          "path": "$.height"
        },
        "timestamp": {
          "path": "$.time"
        }
      }
    }

## Webhook Agents

[[Parse incoming email with Cloudmailin]]

## PostAgents

### Bookmark with GimmeBar

As of 2015-02-20 you can replicate adding a page to Gimme Bar without API access by extracting the relevant cookies/fields from a `POST` request to `https://gimmebar.com/bookmarklet/capture`. Load a page you're going to bookmark, fire up a network inspector (e.g. Chromium's Developer Tools - Network tab) and use the Extension/Bookmarklet to add the page to your gimmebar. You should extract cookies: `gimmebookmarklet` and `gimmebar.session`, and the post field `_csrf`. With these you can setup a PostAgent:

    {
      "post_url": "https://gimmebar.com/bookmarklet/capture",
      "expected_receive_period_in_days": "1",
      "content_type": "form",
      "method": "post",
      "payload": {
        "source": "{{url}}",
        "url": "{{url}}",
        "title": "{{title}}",
        "private": "0",
        "use_prev": "0",
        "_csrf": "REPLACE_ME"
      },
      "headers": {
        "Cookie": "gimmebookmarklet=REPLACE_ME; gimmebar.session=REPLACE_ME"
      },
      "disable_ssl_verification": "true"
    }

## Wunderlist Agent

Make sure you set up a [Wunderlist OAuth Application](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications#wunderlist). Then authenticate against Wunderlist in the `Services` section of your huginn installation.

### XKCD to Wunderlist

In your huginn instance go to `Services` -> `Import Scenario` and enter https://dl.dropboxusercontent.com/u/62784372/xkcd-to-wunderlist.json as the public scenario URL. Select the Wunderlist account you want to use, and confirm that you want to import that scenario.

**Important**: After the import you need to edit the `XKCD Publisher (Wunderlist Agent)`. Click on `Actions` -> `Edit agent` and select the `List` you want to use to store new XKCD Comics.

##Event Formatting Agent - Replace emails in event hash with URL

Easy way to filter and replace content in event using regexp_replace

    {
      "instructions": {
        "message": "{{ content | regex_replace: '(\\S+)@(\\S+).(\\S+)', '{{url}} ' }}"
      }
    } 

## Google Calendar Publisher Agent in conjunction with the JavaScript Agent.

The following (very) long text described a solution, where google calendar entries where created out of data of an email:

[Medium: Automate my marathon training with Huginn](https://medium.com/@chaosspeeder/automate-my-marathon-training-with-huginn-805586cd2d04#.vtvgddonz)

The next example shows a workflow, of creating various Google Calendar entries based on a schedule:

[Medium: Planning my gaming evening with Huginn](https://medium.com/@chaosspeeder/dear-robot-create-my-evening-gaming-plan-b0dd08e596dd#.q3uw7lw1d)
## Flyertalk RSS to Email Alerts

Captures a new post, filters and sends via email:

[[Flyertalk RSS to Email Scenario]]

## Daily updates from Github commits

Get an email digest of commits. Ugly formatting, so please feel free to improve!

[[Daily Update of Huginn Commits on Github]]

## Else-If loops & formatting strings as numbers

Numbers are extracted as strings often and cause issues with comparators. One can either use multiply:1 to cast them as integers or otherwise use string length depending on the goal. Combined with if/elsif/else here:

     {% if total.size >= 7 %}${{total | divided_by:1000000 }}M{% elsif total.size >=6 %}${{round_raised | divided_by:1000}}K{% else %}below $100,000{% endif %}

## Get today's date in Liquid Formatting

This is useful for the subject line in Daily EmailDigestAgent agents

    {% assign current_date = 'now' | date: '%s' %} {{current_date | date: \"%a, %b %d, %Y\" }}

## Amazon Pricewatch

Get an email whenever something drops below a certain price on Amazon

[[Amazon (UK) Product Watch]]