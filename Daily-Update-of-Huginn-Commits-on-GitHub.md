    {
      "schema_version": 1,
      "name": "Github Updates For Huginn",
      "description": "No description provided",
      "source_url": false,
      "guid": "8db013b6e23ef680af48cdcee98e75c4",
      "tag_fg_color": "#ffffff",
      "tag_bg_color": "#5bc0de",
      "icon": null,
      "exported_at": "2016-09-30T16:01:29Z",
      "agents": [
        {
          "type": "Agents::EmailDigestAgent",
          "name": "Huginn Email Digest",
          "disabled": false,
          "guid": "0f405e2af0861e16b75a0564125bec71",
          "options": {
            "subject": "Daily Huginn Updates from GitHub for {% assign current_date = 'now' | date: '%s' %} {{current_date | date: \"%a, %b %d, %Y\" }}",
            "headline": "Latest commits:",
            "expected_receive_period_in_days": "2"
          },
          "schedule": "5am",
          "propagate_immediately": false
        },
        {
          "type": "Agents::RssAgent",
          "name": "Github Huginn RSS",
          "disabled": false,
          "guid": "4b6357c173af9e9efce8e308147876dc",
          "options": {
            "expected_update_period_in_days": "5",
            "clean": "true",
            "url": "https://github.com/cantino/huginn/commits/master.atom"
          },
          "schedule": "every_5h",
          "keep_events_for": 0
        }
      ],
      "links": [
        {
          "source": 1,
          "receiver": 0
        }
      ],
      "control_links": [

      ]
    }
