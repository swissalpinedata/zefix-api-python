# Zefix API in Python: Swiss company register (Handelsregister) and new companies from SHAB

Search the **Swiss commercial register (Zefix, Handelsregister)** by company name and get **new Swiss companies, changes and deletions from the SHAB** as clean JSON with UID, legal form, seat, canton, purpose and capital. The [Zefix Company Register Scraper](https://apify.com/swissalpinedata/swiss-company-register-scraper) on Apify wraps the public Zefix REST API and the amtsblattportal.ch SHAB feed.

Pay per result, no subscription, no login and no proxy setup. New Apify accounts get free monthly credit, which covers a few thousand results.

## Quick start

1. Create a free account on [Apify](https://apify.com) and copy your API token from Settings, Integrations.
2. `export APIFY_TOKEN=your_token`
3. Run one of the examples below.

### Python

```bash
pip install apify-client
python example.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("swissalpinedata/swiss-company-register-scraper").call(run_input={
    "mode": "new-companies",
    "cantons": [
        "ZH"
    ],
    "subRubrics": [
        "HR01"
    ],
    "maxItems": 20
})

for item in client.dataset(run.default_dataset_id).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
node example.mjs
```

```js
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("swissalpinedata/swiss-company-register-scraper").call({
  "mode": "new-companies",
  "cantons": [
    "ZH"
  ],
  "subRubrics": [
    "HR01"
  ],
  "maxItems": 20
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### curl

```bash
curl -X POST "https://api.apify.com/v2/acts/swissalpinedata~swiss-company-register-scraper/run-sync-get-dataset-items" \
  -H "Authorization: Bearer $APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode": "new-companies", "cantons": ["ZH"], "subRubrics": ["HR01"], "maxItems": 20}'
```

## Example output

One record looks like this:

```json
{
  "source": "shab",
  "uid": "CHE-437.038.849",
  "name": "Soul&Science GmbH",
  "legal_form": "Gesellschaft mit beschränkter Haftung",
  "legal_form_code": "0107",
  "seat": "Sigriswil",
  "canton": "BE",
  "status": null,
  "url": "https://www.shab.ch/#!/gazette/publication/75c8e047-49aa-48ec-b9da-389c766cea59",
  "publication_id": "75c8e047-49aa-48ec-b9da-389c766cea59",
  "publication_number": "HR01-1006762303",
  "publication_date": "2026-09-22",
  "sub_rubric": "HR01",
  "language": "de",
  "address": "c/o Sabine Tilmann, Bäreneggweg 8, 3658 Merligen",
  "purpose": "Die Gesellschaft bezweckt das Anbieten und die Durchführung von Aus- und Weiterbildungen, Kursen, Seminaren und Coachings in verschiedenen Lebensbereichen, online und in Präsenz. Ferner bezweckt sie die Entwicklung und den Vertrieb von physischen und digitalen Produkten, die Herausgabe und den Vertrieb von Publikationen sowie den Handel mit Waren aller Art. (...)",
  "capital": 20000.0,
  "capital_currency": "CHF",
  "persons": [
    "Tilmann, Sabine Charlotte Caroline Elisabeth, von Sissach, in Merligen (Sigriswil), Gesellschafterin und Geschäftsführerin, mit Einzelunterschrift, mit 20 Stammanteilen zu je CHF 1'000.00",
    "Tilmann, Elisabeth, von Sissach, in Merligen (Sigriswil), mit Einzelunterschrift"
  ],
  "raw_text": "Soul&Science GmbH, in Sigriswil, CHE-437.038.849, c/o Sabine Tilmann, Bäreneggweg 8, 3658 Merligen, Gesellschaft mit beschränkter Haftung (Neueintragung). Statutendatum: 14.09.2026. Zweck: (...)",
  "scraped_at": "2026-09-22T20:43:14.251379+00:00"
}
```

## What you can build

* B2B leads: every new GmbH and AG in your canton, daily
* KYC and supplier checks by UID
* Enrich a CRM with legal form, seat and purpose
* Market research on company foundations

## Schedules and integrations

On Apify you can save this input as a task, run it on a schedule (for example every morning) and send new results to Google Sheets, Slack, a webhook, Make, n8n or Zapier without writing code. All input fields are documented on the [actor page](https://apify.com/swissalpinedata/swiss-company-register-scraper).

## More Swiss and DACH data APIs

* [swiss-jobs-api](https://github.com/swissalpinedata/swiss-jobs-api): Swiss Jobs API
* [arbeitsagentur-jobs-api](https://github.com/swissalpinedata/arbeitsagentur-jobs-api): Arbeitsagentur Jobsuche API
* [austria-jobs-api](https://github.com/swissalpinedata/austria-jobs-api): Austria Jobs API
* [flatfox-api-python](https://github.com/swissalpinedata/flatfox-api-python): Flatfox API
* [personio-jobs-api](https://github.com/swissalpinedata/personio-jobs-api): Personio, Workable, Recruitee, SmartRecruiters and Teamtailor jobs API in Python and Node

## License

The example code in this repo is MIT licensed. The data comes from public sources; you are responsible for using it in line with the GDPR and the terms of the source sites.
