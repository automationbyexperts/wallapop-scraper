# wallapop Scraper (Spain,Italy,Portugal)

Scrape Wallapop listings at scale across Spain, Italy, and Portugal without writing a single line of code. Paste any Wallapop search URL or item URL, and this actor returns structured data for every listing prices, specs, seller info, images, and engagement metrics.

This repo shows how to call the [wallapop Scraper (Spain,Italy,Portugal)](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/wallapop-scraper on Apify](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/wallapop-scraper](https://automationbyexperts.com/apify/wallapop-scraper)
- **Actor ID for the API:** `fayoussef/wallapop-scraper`

## Use cases

- [Scrape used cars under 5,000 EUR on Wallapop Spain](https://apify.com/fayoussef/wallapop-scraper/examples/used-cars-spain-under-5000?fpr=youssef): Pulls the newest private car listings on Wallapop Spain priced under 5,000 EUR, with price, mileage, year, location and seller details per row. Built for dealers and flippers who want the cheap end of the market in a spreadsheet every morning instead of refreshing the app.
- [Track used car listings on Wallapop Italy](https://apify.com/fayoussef/wallapop-scraper/examples/wallapop-italy-used-cars?fpr=youssef): Exports the latest used car listings from Wallapop Italy into structured rows: price, mileage, year, fuel, location and seller. Set it on a schedule to build a price history of the Italian private market, or run once to size the inventory in a region.
- [Monitor iPhone listings on Wallapop Spain](https://apify.com/fayoussef/wallapop-scraper/examples/iphone-listings-wallapop-spain?fpr=youssef): Watches Wallapop Spain for iPhone 15 listings, newest first, and returns price, condition, location and seller for each. Resellers use it to catch underpriced phones the minute they are posted; schedule it hourly and push new rows to Slack or a sheet.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/wallapop-scraper").call(run_input={'start_urls': [{'url': 'https://es.wallapop.com/search?category_id=100&max_sale_price=5000&order_by=newest'}],
 'max_items': 200,
 'country': 'Spain'})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/wallapop-scraper").call({
    "start_urls": [
        {
            "url": "https://es.wallapop.com/search?category_id=100&max_sale_price=5000&order_by=newest"
        }
    ],
    "max_items": 200,
    "country": "Spain"
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~wallapop-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~wallapop-scraper/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "title": "BMW Serie 2 Gran Tourer 218d Business",
  "price": 18890,
  "currency": "EUR",
  "financed_price": 18490,
  "listing_url": "https://fr.wallapop.com/item/bmw-serie-2-gran-tourer-218d-business-1239358058",
  "share_url": "https://wallapop.com/item/bmw-serie-2-gran-tourer-218d-business-1239358058",
  "brand": "BMW",
  "model": "Serie 2 Gran Tourer",
  "version": "218d Business",
  "year": 2020,
  "km": 114248,
  "engine": "Diesel",
  "gear_box": "Automatic",
  "body_type": "Minivan",
  "doors": 5,
  "seats": 5,
  "horse_power": 150,
  "eco_label": "C",
  "city": "Madrid",
  "postal_code": "28043",
  "country_code": "ES",
  "latitude": 40.462303,
  "longitude": -3.65469,
  "description": "BMW Serie 2 Gran Tourer 218d Business, Automático | 7 plazas | Muy equipado",
  "images": [
    "https://cdn.wallapop.com/images/10420/kh/vq/__/c10420p1239358058/i6368481882.jpg?pictureSize=W640",
    "https://cdn.wallapop.com/images/10420/kh/vq/__/c10420p1239358058/i6368481903.jpg?pictureSize=W640"
  ],
  "views": 52,
  "favorites": 3,
  "conversations": 0,
  "seller_id": "8x6q9kq5p5zy",
  "seller_is_top_profile": false,
  "seller_legal_name": "second cars luxury sl",
  "seller_commercial_registry": "second cars luxury",
  "seller_registration_number": "b67661009",
  "seller_email": "secondcarsluxury@gmail.com",
  "seller_phone": "912175139",
  "seller_self_certification": "This seller has declared to only offer products or services that comply with applicable European regulations.",
  "shipping_available": false,
  "category": "Cars",
  "category_id": "100",
  "extra_attributes": {
    "warranty": "12"
  },
  "item_id": "8j38g9o9pyz9",
  "slug": "bmw-serie-2-gran-tourer-218d-business-1239358058",
  "type": "car",
  "modified_date": 1776625796
}
```

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [Fnac.com Scraper: Prices, EAN, Stock, Sellers & Reviews](https://github.com/automationbyexperts/fnac-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Business Phones, Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
