[France Travail Scraper](https://apify.com/santamaria-automations/france-travail-scraper?fpr=data)

# France Travail Job Scraper

Scrape job listings from **France Travail** (formerly Pole Emploi), France's public employment service with 500,000+ active job listings. Extract title, company, location, contract type, salary, and full description.

HTTP-only scraper using Cheerio (no browser). Runs at 128MB memory.

---

## Scraper d'offres d'emploi France Travail

Scrapez les offres d'emploi de **France Travail** (anciennement Pole Emploi), le service public de l'emploi en France avec plus de 500 000 offres actives. Extrayez le titre, l'entreprise, la localisation, le type de contrat, le salaire et la description complete.

## Use with AI Agents (MCP)

Connect this actor to any MCP-compatible AI client — Claude Desktop, Claude.ai, Cursor, VS Code, LangChain, LlamaIndex, or custom agents.

**Apify MCP server URL:**

```
https://mcp.apify.com?tools=santamaria-automations/france-travail-scraper
```

**Example prompt once connected:**

> "Use `france-travail-scraper` to scrape job listings from france travail. Return results as a table."

Clients that support dynamic tool discovery (Claude.ai, VS Code) will receive the full input schema automatically via `add-actor`.

## Related Actors

Looking for more job data? Check out our other scrapers:

**Global**

- [LinkedIn Jobs Scraper](https://apify.com/santamaria-automations/linkedin-scraper)
- [Indeed Scraper](https://apify.com/santamaria-automations/indeed-scraper)

**DACH Region**

- [Jobs.ch Scraper](https://apify.com/santamaria-automations/jobs-ch-scraper)
- [StepStone.de Scraper](https://apify.com/santamaria-automations/stepstone-de-scraper)
- [Karriere.at Scraper](https://apify.com/santamaria-automations/karriere-at-scraper)

**Nordics**

- [Arbetsformedlingen.se Scraper](https://apify.com/santamaria-automations/arbetsformedlingen-se-scraper) -- Swedish jobs
- [Jobindex.dk Scraper](https://apify.com/santamaria-automations/jobindex-dk-scraper) -- Danish jobs

**UK**

- [Reed.co.uk Scraper](https://apify.com/santamaria-automations/reed-uk-scraper) -- UK jobs

**Enrich your job data**

- [Website Job Extractor](https://apify.com/santamaria-automations/website-job-extractor)
- [Website Contact Extractor](https://apify.com/santamaria-automations/website-contact-extractor)

---

## Features

- **500,000+ active listings** from France's largest public job board
- **Multi-query support** -- run multiple search keywords in one execution, deduplicated
- **SERP + Detail modes** -- fast SERP-only or full detail extraction with salary and remote info
- **French contract types** -- CDI, CDD, interim, alternance, stage
- **Remote detection** -- detects teletravail (remote work) mentions
- **Salary parsing** -- structured min/max from French salary formats (annuel, mensuel, horaire)
- **Location filtering** -- filter by department code (75 = Paris, 69 = Lyon, etc.)
- **Low cost** -- 128MB memory, HTTP-only

## Output Fields

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | France Travail offer ID |
| `title` | string | Job title |
| `company` | string/null | Hiring company name |
| `location` | string | Job location (city, department) |
| `country` | string | Always "FR" |
| `employment_type` | string/null | full-time, temporary, internship, etc. |
| `remote_option` | string/null | remote, hybrid, or null |
| `salary_min` | number/null | Minimum salary (EUR) |
| `salary_max` | number/null | Maximum salary (EUR) |
| `salary_text` | string/null | Salary as displayed |
| `description_snippet` | string/null | Short description (max 500 chars) |
| `description_full` | string/null | Full description (detail mode only) |
| `posted_at` | string/null | Publication date |
| `source_url` | string | France Travail listing URL |
| `source_platform` | string | Always "francetravail.fr" |
| `search_query` | string/null | The search keyword that found this job |
| `scraped_at` | string | Scrape timestamp (ISO 8601) |

## Input Examples

### Basic search

```
{
  "searchQuery": "developpeur",
  "maxResults": 50
}
```

### Multi-query with location

```
{
  "searchQueries": ["developpeur", "ingenieur", "data scientist"],
  "location": "75",
  "maxResults": 200,
  "maxResultsPerQuery": 100
}
```

### With full details (salary + description)

```
{
  "searchQueries": ["developpeur python"],
  "includeDetails": true,
  "maxResults": 50
}
```

## Pricing

| Event | Price (USD) | Description |
| --- | --- | --- |
| `job-start` | $0.05 | Per actor run |
| `job-serp-result` | $0.003 | Per job listing from search results |
| `job-detail-result` | $0.008 | Per job detail page fetched |