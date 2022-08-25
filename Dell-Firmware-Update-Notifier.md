Retrieves current firmware lists from Dell in json format and filters for new BIOS changes.
Update URL/ProductCode to suit your product
```json
{
  "schema_version": 1,
  "name": "Dell Firmware Update",
  "description": "Check Dell Support for Updated BIOS Files",
  "source_url": false,
  "guid": "d4b61d77eaacbcde35b34ec61cdc20ad",
  "tag_fg_color": "#ffffff",
  "tag_bg_color": "#5bc0de",
  "icon": "gear",
  "exported_at": "2019-11-16T01:00:36Z",
  "agents": [
    {
      "type": "Agents::WebsiteAgent",
      "name": "Dell Firmware",
      "disabled": false,
      "guid": "e98895d82a992c7222a8b85736596f18",
      "options": {
        "expected_update_period_in_days": "2",
        "url": "https://www.dell.com/support/driver/au/en/aubsd1/ips/api/driverlist/getdriversbyproduct?productcode=latitude-e7250-ultrabook&oscode=BIOSA",
        "type": "json",
        "mode": "on_change",
        "extract": {
          "DriverName": {
            "path": "DriverListProductData[*].DriverName",
            "hidden": true
          },
          "Type": {
            "path": "DriverListProductData[*].Type"
          },
          "ReleaseDate": {
            "path": "DriverListProductData[*].ReleaseDate",
            "hidden": true
          },
          "FileName": {
            "path": "DriverListProductData[*].FileFrmtInfo.FileName",
            "hidden": true
          },
          "HttpFileLocation": {
            "path": "DriverListProductData[*].FileFrmtInfo.HttpFileLocation",
            "hidden": true
          }
        },
        "template": {
          "subject": "{{DriverName}} Update",
          "body": "<a href='{{HttpFileLocation}}'>{{FileName}}</a> Available<br>Released {{ReleaseDate}}"
        }
      },
      "schedule": "every_7d",
      "keep_events_for": 0,
      "propagate_immediately": false
    },
    {
      "type": "Agents::TriggerAgent",
      "name": "Dell Firmware Filter",
      "disabled": false,
      "guid": "eef28e9c569690cabac102caee7249d3",
      "options": {
        "expected_receive_period_in_days": "2",
        "keep_event": "true",
        "rules": [
          {
            "type": "field==value",
            "value": "TYPE_BIOS",
            "path": "Type"
          }
        ]
      },
      "keep_events_for": 172800,
      "propagate_immediately": false
    },
    {
      "type": "Agents::EmailAgent",
      "name": "Email Direct",
      "disabled": false,
      "guid": "f2911189ed5fb000d20f878f6e7c5463",
      "options": {
        "subject": "{{subject}}",
        "expected_receive_period_in_days": "2",
        "body": "{{body}}"
      },
      "propagate_immediately": false
    }
  ],
  "links": [
    {
      "source": 0,
      "receiver": 1
    },
    {
      "source": 1,
      "receiver": 2
    }
  ],
  "control_links": [

  ]
}
```