# Agent Configuration Examples

## WebsiteAgents

### Hacker News searcher

Look for new Hacker News posts that mention SF or "Bay Area"

    {
      "expected_update_period_in_days": 2,
      "url": "http://api.thriftdb.com/api.hnsearch.com/items/_search?q=francisco+OR+sf+OR+%22bay+area%22&sortby=create_ts%20desc",
      "type": "json",
      "mode": "on_change",
      "extract": {
        "item": {
          "path": "results[*].item",
          "attr": "src"
        }
      }
    }

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
          "text": true
        },
        "url": {
          "css": "item link",
          "text": true
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
