`{
  "schema_version": 1,
  "name": "Flyertalk Mileage Run Alert",
  "description": "No description provided",
  "source_url": false,
  "guid": "e2582e979bc1b93044dc59fb82d1b152",
  "tag_fg_color": "#ffffff",
  "tag_bg_color": "#5bc0de",
  "exported_at": "2016-02-07T12:21:32Z",
  "agents": [
    {
      "type": "Agents::EmailAgent",
      "name": "Flyertalk Email Alert Agent",
      "disabled": false,
      "guid": "1ad7b7eff52857a9f7c45571e2956277",
      "options": {
        "subject": "Flyertalk: {{title}}",
        "headline": "New post",
        "expected_receive_period_in_days": "15",
        "body": "Post: {{message}}"
      },
      "propagate_immediately": true
    },
    {
      "type": "Agents::TriggerAgent",
      "name": "Home Airports Filter for Flyertalk",
      "disabled": false,
      "guid": "24e45c58615b94ba186335d78775c5e7",
      "options": {
        "expected_receive_period_in_days": "2",
        "keep_event": "false",
        "rules": [
          {
            "type": "regex",
            "value": "(lhr|london)",
            "path": "title"
          }
        ],
        "message": "<a href=\"{{url}}\">{{title}}</a> {{description}}"
      },
      "keep_events_for": 15552000,
      "propagate_immediately": true
    },
    {
      "type": "Agents::RssAgent",
      "name": "Flyertalk RSS Agent",
      "disabled": false,
      "guid": "6663283a70d08ce6b24ab68908212e7f",
      "options": {
        "expected_update_period_in_days": "5",
        "clean": "true",
        "url": "http://www.flyertalk.com/forum/external.php?type=RSS2&forumids=372"
      },
      "schedule": "every_10m",
      "keep_events_for": 31536000
    }
  ],
  "links": [
    {
      "source": 1,
      "receiver": 0
    },
    {
      "source": 2,
      "receiver": 1
    }
  ],
  "control_links": [

  ]
}`