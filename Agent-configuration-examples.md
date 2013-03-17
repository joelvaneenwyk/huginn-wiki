# Agent Configuration Examples

## WebsiteAgents

Look for new Hacker News posts that mention SF or "Bay Area"

    {
      "expected_update_period_in_days": "2",
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