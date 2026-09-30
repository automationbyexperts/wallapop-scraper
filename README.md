# Wallapop Scraper: Listings, Prices & Seller Phone Numbers from Spain, France, Italy, Portugal & UK

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef)
![Markets](https://img.shields.io/badge/Markets-ES%20%7C%20FR%20%7C%20IT%20%7C%20PT%20%7C%20UK-2ea44f)
![Seller](https://img.shields.io/badge/Seller-phone%20and%20email-1C7ED6)
![Engagement](https://img.shields.io/badge/Engagement-views%20%7C%20favorites-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Wallapop Scraper on Apify](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef)
> Scrape **Wallapop** second-hand listings from Spain, France, Italy, Portugal and the UK with price, car and item specs, **seller business info, phone and email**, views, favorites, GPS and photos. Paste any Wallapop search or item URL.

**Wallapop Scraper** turns Wallapop, Southern Europe's biggest second-hand marketplace, into clean structured data from all five markets. It is built for used car dealers, resellers, price comparison sites and market researchers. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/wallapop-scraper on Apify](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/wallapop-scraper](https://automationbyexperts.com/apify/wallapop-scraper)
- **Actor ID for the API:** `fayoussef/wallapop-scraper`

## What the Wallapop scraper does

- **Five markets, one Actor**: es.wallapop.com, fr.wallapop.com, it.wallapop.com, pt.wallapop.com and the UK site.
- **Every category**: cars and motorbikes, phones and electronics, fashion, home, real estate...
- **Seller details**: business name, registration and VAT number, email and phone for business sellers.
- **Engagement data**: views, favorites and conversations per listing.
- **Automatic geo anchoring**: a URL without coordinates is centred on the country (Madrid, Paris...), or set your own latitude and longitude.
- **Filters from the URL**: price range, distance, brand, model, seller type and every other Wallapop filter pass straight through.

## Output fields: what data you get

One row per listing. The main fields:

| Field | Description |
|---|---|
| `title` / `listing_url` / `description` / `category` | Listing identity |
| `price` / `financed_price` / `currency` | Cash and financed price |
| `brand` / `model` / `version` / `year` / `km` | Car and item attributes |
| `engine` / `gear_box` / `body_type` / `horse_power` / `eco_label` | Car specs |
| `city` / `postal_code` / `latitude` / `longitude` | Location and GPS |
| `seller_phone` / `seller_email` | Seller contact |
| `seller_legal_name` / `seller_registration_number` | Business seller identity and VAT number |
| `views` / `favorites` / `conversations` | Engagement |
| `images` / `shipping_available` | Photos and shipping |

## Input

Paste Wallapop URLs and optionally set the location:

| Field | What it does |
|---|---|
| `start_urls` | Wallapop search or item URLs from any of the five markets |
| `max_items` | Maximum number of listings |
| `country` | Default country when the URL has no location |
| `latitude` / `longitude` | Optional exact search centre |

## Use cases

- **Used car dealers**: track private and dealer car prices on Wallapop Spain and Italy.
- **Resellers**: find underpriced phones, consoles and electronics to flip.
- **Price comparison**: aggregate second-hand prices across five countries.
- **Lead generation**: contact business sellers by phone or email.
- **Fraud and compliance**: check business registration numbers of sellers.

Ready-made examples you can run in one click:

- [Scrape used cars under 5,000 EUR on Wallapop Spain](https://apify.com/fayoussef/wallapop-scraper/examples/used-cars-spain-under-5000?fpr=youssef): Pulls the newest private car listings on Wallapop Spain priced under 5,000 EUR, with price, mileage, year, location and seller details per row. Built for dealers and flippers who want the cheap end of the market in a spreadsheet every morning instead of refreshing the app.
- [Monitor iPhone listings on Wallapop Spain](https://apify.com/fayoussef/wallapop-scraper/examples/iphone-listings-wallapop-spain?fpr=youssef): Watches Wallapop Spain for iPhone 15 listings, newest first, and returns price, condition, location and seller for each. Resellers use it to catch underpriced phones the minute they are posted; schedule it hourly and push new rows to Slack or a sheet.

## Quick start

### 1. In the browser (no code)

1. Search on Wallapop with your filters and copy the URL.
2. Open the Actor on Apify, click **Try for free** and paste the URL into **Start URLs**.
3. Click **Start**, then download Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

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

#### JavaScript / Node.js

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

#### cURL (plain HTTP)

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

## Integrations and automation

- **Schedule it** hourly or daily to catch new listings before they sell.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Does Wallapop have a public API?
No. This Actor is a Wallapop API alternative: one Apify API call returns structured JSON for every listing.

### Which Wallapop countries are supported?
Spain, France, Italy, Portugal and the United Kingdom.

### Does it return the seller phone number?
Yes, `seller_phone` and `seller_email` where Wallapop publishes them, mainly for business sellers.

### How do I filter by price, distance or brand?
Set the filters on Wallapop, then paste the URL. Every Wallapop URL parameter is passed through.

### Can I scrape a single item?
Yes. Paste a `wallapop.com/item/...` URL.

### Can I scrape used cars on Wallapop?
Yes. Car listings include brand, model, year, km, engine, gearbox, power and eco label.

### What output formats are available?
JSON, CSV, Excel and XML from the Apify dataset, or through the API.

## Scraper de Wallapop en español

El **Wallapop Scraper** extrae anuncios de Wallapop en España, Francia, Italia, Portugal y Reino Unido: precio, datos de coches y artículos, **teléfono y email del vendedor**, visitas, favoritos, GPS y fotos. Pegue una URL de búsqueda de Wallapop y descargue los resultados en Excel, CSV o JSON. [Probar en Apify](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef).

## Scraper Wallapop in italiano

Il **Wallapop Scraper** estrae gli annunci di Wallapop Italia e degli altri mercati con prezzo, dati di auto e articoli, **telefono ed email del venditore**, visualizzazioni, preferiti, GPS e foto, esportabili in Excel, CSV o JSON. [Provalo su Apify](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef).

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [Fnac.com Scraper: Prices, EAN, Stock & Reviews](https://github.com/automationbyexperts/fnac-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Real Estate Listings](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Phone Numbers & Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/wallapop-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
