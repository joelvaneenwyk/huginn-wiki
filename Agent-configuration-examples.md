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
<code>
{
  "instructions": {
    "message": "{{ content | regex_replace: '(\\S+)@(\\S+).(\\S+)', ' ' }}  ",
  },
  "matchers": [

  ],
  "mode": "clean"
} 
</code>