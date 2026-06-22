[France Travail Scraper](https://apify.com/unfenced-group/france-travail-scraper?fpr=data)

# France Travail Scraper

![France Travail Scraper](https://images.apifyusercontent.com/TMlNvPj270PMG_34ZJajDPLMGgM6Q2sSL0mrRDjmK1g/w:1800/cb:1/aHR0cHM6Ly9pLmltZ3VyLmNvbS9iR3EySjFNLnBuZw.webp)

Scrape structured job listings from [France Travail](https://www.francetravail.fr) — France. 400,000+ active listings. No API key required.

---

## Why this scraper?

### 🏛️ France's official employment service — 400,000+ listings

France Travail (formerly Pôle Emploi) is the French national employment agency with the largest database of French job vacancies.

### 📄 Full job descriptions

Enable `fetchDetails` to retrieve complete job descriptions in all three formats.

### 📋 NAF / ROME codes

French occupational classification codes (ROME) included where available.

### 🔄 Repost detection

Cross-run deduplication with a 90-day TTL. Use `skipReposts: true` for new-only feeds.

### 🔗 Direct URL scraping

Supply specific France Travail search or category URLs via `startUrls`.

### ⚙️ No API key required

Runs without any third-party credentials.

---

## Input parameters

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `maxItems` | integer | Maximum number of results to return. | `5` |
| `skipReposts` | boolean | Skip listings already seen in previous runs (90-day deduplication window). | `false` |

---

## Output schema

Each result contains the following fields.

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | Unique job listing ID from the source platform. |
| `url` | string | Direct URL to the job listing. |
| `title` | string | Job title as published. |
| `company` | string | Employer / company name. |
| `location` | string | Full location string as published. |
| `city` | string | City of the work location. |
| `country` | string | Country code (ISO 3166-1 alpha-2). |
| `contractType` | string | Contract type (permanent, contract, temporary, etc.). |
| `workSchedule` | string | Work schedule (full-time, part-time, etc.). |
| `salaryMin` | number | Minimum salary (null if not published by employer). |
| `salaryMax` | number | Maximum salary (null if not published by employer). |
| `salaryCurrency` | string | ISO 4217 currency code (null if no salary published). |
| `salaryPeriod` | string | Salary period: YEAR / MONTH / WEEK / DAY / HOUR. |
| `publishDate` | string | Publication date (YYYY-MM-DD). |
| `publishDateISO` | string | Publication date in ISO 8601 format. |
| `source` | string | Source domain name. |
| `scrapedAt` | string | ISO 8601 timestamp of when this item was scraped. |
| `contentHash` | string | MD5 hash of key fields for change detection (16 chars). |
| `summary` | string | Human-readable one-line summary of the listing. |
| `changeStatus` | string | Change status: NEW / MODIFIED / UNCHANGED. |
| `isRepost` | boolean | True if this listing was seen in a previous run (90-day window). |
| `originalPublishDate` | string | Original publish date if this is a repost (null otherwise). |
| `originalUrl` | string | Original URL if this is a repost (null otherwise). |

**Example output record:**

```
{
  "id": "123456",
  "url": "https://www.francetravail.fr/jobs/senior-developer/123456",
  "title": "Développeur Web",
  "company": "La Poste",
  "location": "Paris",
  "city": "Paris",
  "country": "FR",
  "contractType": "Permanent",
  "workSchedule": "Full-time",
  "salaryMin": 45000,
  "salaryMax": 60750,
  "salaryCurrency": "EUR",
  "salaryPeriod": "YEAR",
  "publishDate": "2026-04-15",
  "publishDateISO": "2026-04-15",
  "source": "francetravail.fr",
  "scrapedAt": "2026-04-24T09:00:00.000Z",
  "contentHash": "a3f1b2c4d5e67890",
  "summary": "Développeur Web · La Poste · Paris",
  "changeStatus": "NEW",
  "isRepost": false,
  "originalPublishDate": null,
  "originalUrl": null
}
```

---

## Examples

### 1 — Search for Développeur Web roles in Paris

```
{
  "searchQuery": "d\u00e9veloppeur",
  "maxResults": 100
}
```

### 2 — All listings without filters

```
{
  "searchQuery": "",
  "maxResults": 500
}
```

### 3 — Scrape a specific search page directly via startUrls

```
{
  "startUrls": [
    {
      "url": "https://www.francetravail.fr/jobs?q=d\u00e9veloppeur"
    }
  ],
  "maxResults": 50
}
```

### 4 — Daily feed — new listings only, past 24 hours, no reposts

```
{
  "searchQuery": "",
  "skipReposts": true,
  "maxResults": 1000
}
```

---

## 💰 Pricing

**$1.50 per 1,000 results** — you only pay for successfully retrieved listings.
Failed retries and filtered reposts are never charged.

| Results | Cost |
| --- | --- |
| 100 | ~$0.15 |
| 1,000 | ~$1.50 |
| 10,000 | ~$15.00 |
| 100,000 | ~$150.00 |

> Flat-rate alternatives typically charge $29–$49/month regardless of usage.

Use the **Max results** cap in the input to control your spend exactly.

---

## Performance

| Run size | Approx. time |
| --- | --- |
| 100 listings | ~2 min |
| 1,000 listings | ~15 min |
| 10,000 listings | ~2.5 hours |

---

## Known limitations

- **Salary:** Not all employers publish salary information — `salaryMin` and `salaryMax` may be `null`.
- **fetchDetails:** Setting `fetchDetails: false` returns list-page fields only; description fields will be `null`.

---

## Technical details

- **Source:** francetravail.fr — France's job market
- **Memory:** 256 MB
- **Repost storage:** KeyValueStore `france-travail-job-dedup`, 90-day TTL
- **Retry:** Automatic retry on network errors, exponential backoff, 3 attempts per request

---

## Additional services

Need a custom actor, additional filters, scheduled runs, or integration support?
Send an email to [info@unfencedgroup.nl](mailto:info@unfencedgroup.nl) — we build on request.

---

*Part of the [Unfenced Group](https://apify.com/unfenced-group) European job board scraper portfolio — 50+ job markets covered.*
*Built by [unfenced-group](https://apify.com/unfenced-group) · Issues? Open a ticket or send a message.*