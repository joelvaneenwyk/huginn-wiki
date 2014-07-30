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