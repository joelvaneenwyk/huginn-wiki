    {
        "schema_version": 1,
        "name": "Amazon Toner",
        "description": "No description provided",
        "source_url": false,
        "guid": "937f937533d4a490a02781381a763bf3",
        "tag_fg_color": "#ffffff",
        "tag_bg_color": "#5bc0de",
        "icon": "gear",
        "exported_at": "2016-10-03T16:58:25Z",
        "agents": [
            {
                "type": "Agents::EmailAgent",
                "name": "Amazon Toner Email Agent",
                "disabled": false,
                "guid": "230a06d95b01efcbd24f4f7b332506dc",
                "options": {
                    "subject": "Amazon Toner On Sale",
                    "headline": "",
                    "expected_receive_period_in_days": "90",
                    "body": "{{body_text}}"
                },
                "propagate_immediately": true
            },
            {
                "type": "Agents::WebsiteAgent",
                "name": "Amazon Toner Website Agent",
                "disabled": false,
                "guid": "2c1ea904fea73164ac69fe5ba657a5db",
                "options": {
                    "expected_update_period_in_days": "90",
                    "url": [
                        "https://www.amazon.co.uk/HP-Original-LaserJet-Cartridge-C9733A/dp/B000077CF6/",
                        "https://www.amazon.co.uk/Hewlett-Packard-HP-Laser-Toner/dp/B00AVYYRE0/"
                    ],
                    "type": "html",
                    "mode": "on_change",
                    "extract": {
                        "body_text": {
                            "xpath": "//*[@id=\"priceblock_ourprice\"]",
                            "value": "substring-after(.,\"£\")"
                        },
                        "url": {
                            "xpath": "//link[@rel='canonical']/@href",
                            "value": "."
                        },
                        "color": {
                            "xpath": "//*[@id=\"variation_color_name\"]/div/span",
                            "value": "normalize-space(.)"
                        }
                    }
                },
                "schedule": "every_1h",
                "keep_events_for": 0,
                "propagate_immediately": true
            },
            {
                "type": "Agents::WebsiteAgent",
                "name": "Amazon Toner Website Agent Yellow",
                "disabled": false,
                "guid": "e7e4f3cfde6a14cbf8e7ec6ab6570772",
                "options": {
                    "expected_update_period_in_days": "90",
                    "url": [
                        "https://www.amazon.co.uk/HP-Original-C9732A-Laserjet-Cartridge/dp/B000077CF5/"
                    ],
                    "type": "html",
                    "mode": "on_change",
                    "extract": {
                        "body_text": {
                            "xpath": "//*[@id=\"priceblock_ourprice\"]",
                            "value": "substring-after(.,\"£\")"
                        },
                        "url": {
                            "xpath": "//link[@rel='canonical']/@href",
                            "value": "."
                        },
                        "color": {
                            "xpath": "//*[@id=\"prodDetails\"]/div/div[1]/div/div[2]/div/div/table/tbody/tr[5]/td[2]",
                            "value": "normalize-space(.)"
                        }
                    }
                },
                "schedule": "every_1h",
                "keep_events_for": 0,
                "propagate_immediately": true
            },
            {
                "type": "Agents::TriggerAgent",
                "name": "Amazon Toner Trigger Agent",
                "disabled": false,
                "guid": "eaf805c6260c26c948bf291608e2ceb5",
                "options": {
                    "expected_receive_period_in_days": "1",
                    "keep_event": "false",
                    "rules": [
                        {
                            "type": "field<value",
                            "value": "99",
                            "path": "body_text"
                        }
                    ],
                    "message": "{{agent}} toner on sale for {{body_text}}. <a href=\"{{url}}\">{{url}}</a>"
                },
                "keep_events_for": 0,
                "propagate_immediately": true
            },
            {
                "type": "Agents::EventFormattingAgent",
                "name": "Amazon Toner Formatting",
                "disabled": false,
                "guid": "f3b7087e155ec7d9c4a5898d06f33615",
                "options": {
                    "instructions": {
                        "message": "Amazon Toner On Sale",
                        "agent": "{{color}}",
                        "subject": "{{body_text}}",
                        "body_text": "{{body_text}}",
                        "url": "{{url}}"
                    },
                    "matchers": [

                    ],
                    "mode": "clean"
                },
                "keep_events_for": 0,
                "propagate_immediately": true
            }
        ],
        "links": [
            {
                "source": 1,
                "receiver": 4
            },
            {
                "source": 2,
                "receiver": 4
            },
            {
                "source": 3,
                "receiver": 0
            },
            {
                "source": 4,
                "receiver": 3
            }
        ],
        "control_links": [

        ]
    }