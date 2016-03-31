{
	  "schema_version": 1,
	  "name": "Github Updates For Huginn",
	  "description": "No description provided",
	  "source_url": false,
	  "guid": "8db013b6e23ef680af48cdcee98e75c4",
	  "tag_fg_color": "#ffffff",
	  "tag_bg_color": "#5bc0de",
	  "exported_at": "2016-03-31T14:56:49Z",
	  "agents": [
	    {
	      "type": "Agents::WebsiteAgent",
	      "name": "Github Huginn",
	      "disabled": false,
	      "guid": "0adf3a6dd5a3613196ecbdd099265015",
	      "options": {
	        "expected_update_period_in_days": "7",
	        "url": "https://github.com/cantino/huginn/commits/master",
	        "type": "html",
	        "mode": "on_change",
	        "extract": {
	          "body_text": {
	            "css": "li.commit.commits-list-item.table-list-item.js-navigation-item.js-details-container.js-socket-channel.js-updatable-content",
	            "value": ".//text()[last()]"
	          }
	        }
	      },
	      "schedule": "every_2h",
	      "keep_events_for": 0,
	      "propagate_immediately": false
	    },
	    {
	      "type": "Agents::EmailDigestAgent",
	      "name": "Huginn Email Digest",
	      "disabled": false,
	      "guid": "0f405e2af0861e16b75a0564125bec71",
	      "options": {
	        "subject": "Latest Huginn Updates",
	        "headline": "Latest commits:",
	        "expected_receive_period_in_days": "2"
	      },
	      "schedule": "5am",
	      "propagate_immediately": false
	    }
	  ],
	  "links": [
	    {
	      "source": 0,
	      "receiver": 1
	    }
	  ],
	  "control_links": [

	  ]
	}