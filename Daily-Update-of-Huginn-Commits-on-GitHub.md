    {
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
      }
    }
    }