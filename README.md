[France Travail Scraper](https://apify.com/fatihtahta/france-travail-scraper?fpr=data)

# France Travail Scraper

**Slug:** fatihtahta/france-travail-scraper

## Overview

France Travail Scraper collects structured job listing data from [France Travail](https://francetravail.fr), including core job attributes such as listing ID, title, company, location, publication date, contract details, salary details, skills, and employer information when available. It is designed for teams that need consistent job market data without manually searching and exporting listings one by one. [France Travail](https://francetravail.fr) is France's national employment platform, making it a valuable source for labor market visibility, hiring activity, and role-level demand signals across regions and sectors. The actor automates recurring collection so you can build datasets faster, reduce manual work, and keep results consistent across runs. It is well suited for reporting, enrichment, monitoring, and operational workflows that depend on clean JSON output.

## Why Use This Actor

- **Market researchers and analysts:** Track hiring volume, salary ranges, contract mix, and regional demand for roles such as logistics, IT, healthcare, or hospitality.
- **Product and content teams:** Discover trending job titles, skill requirements, and employer language to inform content calendars, landing pages, or audience research.
- **Developers and data engineers:** Feed structured job data into dashboards, warehouses, alerts, ETL pipelines, or internal search and matching systems.
- **Lead generation and enrichment teams:** Identify employers, recruiters, and job-level context that can support prospect research or company enrichment workflows.
- **Monitoring and competitive intelligence teams:** Watch how hiring activity changes over time by location, contract type, publication recency, or selected job categories.

## Input Parameters

Provide any combination of URLs, queries, and filters to define the job listings you want to collect.

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `queries` | `string[]` | Search keywords to run as separate job searches, such as job titles, skills, or hiring phrases. Example values: `data analyst`, `cariste`, `assistant comptable`. | – |
| `location` | `string` | A city, department, region, or postal area applied to all searches. Leave empty to search across France. | – |
| `published_date` | `string` | Publication recency filter. Allowed values: `Last 24 hours`, `Last 3 Days`, `Last Week`, `Last 2 Weeks`, `Last Month`. | – |
| `contract_type` | `string[]` | Employment contract types to include. Allowed values: `Permanent contract (CDI) | CDI`, `Fixed-term contract (CDD) | CDD`, `Temporary work (Interim) | Intérim`, `Permanent temp contract | CDI Intérimaire`, `Seasonal work | Saisonnier`, `Apprenticeship contract | Contrat apprentissage`, `Professional training contract | Cont. professionnalisation`, `Pre-employment training program | Prépa.opérationnel.emploi`, `Project-based permanent contract | CDI de chantier ou d'opération`, `Educational engagement contract | Contrat d'Engagement Educatif`, `Intermittent contract | Contrat intermittent`, `PACTE contract | Contrat pacte`, `Usage-based contract | Contrat d'usage`, `Subsidized employment contract (CAE) | CUI - CAE`, `Subsidized employment contract (CIE) | CUI - CIE`, `Military reserve service commitment | Engagement à servir dans la réserve`, `Franchise / self-employed license | Franchise`, `Economic integration program | Insertion par l'activ.éco.`, `Umbrella company employment | Portage salarial`, `Commercial profession | Profession commerciale`, `Liberal profession / independent professional | Profession libérale`, `Business takeover | Reprise d'entreprise`. | – |
| `contract_duration` | `string[]` | Working time filters. Allowed values: `Full-time | Temps plein`, `Part-time | Temps partiel`, `Not specified | Non renseignée`. | – |
| `job_category` | `string[]` | Professional domains to include. Allowed values: `Procurement | Achats, Comptabilité, Gestion`, `Arts | Arts, Artisanat d'art`, `Finance | Banque, Assurance`, `Construction | Bâtiment, Travaux Publics`, `Sales | Commerce, Vente`, `Communication | Communication, Multimédia`, `Consulting | Conseil, Etudes`, `Management | Direction d'entreprise`, `Agriculture | Espaces verts et naturels, Agriculture, Pêche, Soins aux animaux`, `Hospitality | Hôtellerie - Restauration, Tourisme, Animation`, `Real estate | Immobilier`, `Industry | Industrie`, `IT | Informatique, Télécommunication`, `Maintenance | Installation, Maintenance`, `Marketing | Marketing, Stratégie commerciale`, `HR | Ressources Humaines`, `Healthcare | Santé`, `Administrative | Secrétariat, Assistanat`, `Services | Services à la personne, à la collectivité`, `Entertainment | Spectacle`, `Sports | Sport`, `Logistics | Transport, Logistique`. | – |
| `min_salary` | `integer` | Minimum monthly gross salary to keep in results. Must be at least `1`. | – |
| `experience` | `string[]` | Experience requirements to include. Allowed values: `Entry-level | Moins de 1 an`, `Mid-level | De 1 à 3 ans`, `Senior | Plus de 3 ans`, `Not specified | Non renseignée`. | – |
| `seniority` | `string[]` | Qualification level filter. Allowed values: `Executive | Cadre`, `Non-executive | Non cadre`, `Not specified | Non renseignée`. | – |
| `only_france_travail` | `boolean` | When `true`, keeps only listings published directly on France Travail rather than partner listings. | `false` |
| `early_application` | `boolean` | When `true`, focuses on listings with lower visible application count to surface less competitive opportunities. | `false` |
| `inclusive_employer` | `boolean` | When `true`, keeps only listings from employers that display a disability-inclusion commitment. | `false` |
| `adapted_company` | `boolean` | When `true`, keeps only listings from adapted companies. | `false` |
| `sort_by` | `string` | Result sorting mode. Allowed values: `Most relevant | Pertinence`, `Newest | Date`. | – |
| `maximize_coverage` | `boolean` | When `true`, broad searches are expanded to recover more matching listings from larger result sets while preserving your selected filters. | `true` |
| `limit` | `integer` | Maximum number of listings to save for each query. Use smaller values for testing and larger values for fuller collection. Must be at least `1`. | – |
| `proxyConfiguration` | `object` | Apify proxy and connection settings for more reliable collection on longer or larger runs. Most users can keep the default configuration. | Apify Proxy with `RESIDENTIAL` group |

## Example Inputs

### Scenario: query-driven monitoring run

```
{
  "queries": ["data analyst", "business analyst"],
  "location": "Paris",
  "published_date": "Last Week",
  "contract_type": ["Permanent contract (CDI) | CDI"],
  "sort_by": "Newest | Date",
  "limit": 300
}
```

### Scenario: targeted category and salary run

```
{
  "queries": ["cariste"],
  "location": "Lille",
  "job_category": ["Logistics | Transport, Logistique"],
  "contract_duration": ["Full-time | Temps plein"],
  "min_salary": 2000,
  "experience": ["Mid-level | De 1 à 3 ans"],
  "limit": 150
}
```

### Scenario: inclusive employer sourcing run

```
{
  "queries": ["assistant administratif"],
  "location": "Lyon",
  "only_france_travail": true,
  "inclusive_employer": true,
  "adapted_company": true,
  "early_application": true,
  "maximize_coverage": true,
  "limit": 100
}
```

## Output

### 6.1 Output destination

The actor writes results to an Apify dataset as JSON records. And the dataset is designed for direct consumption by analytics tools, ETL pipelines, and downstream APIs without post-processing.

### 6.2 Record envelope (all items)

For primary job listing records, the stable record envelope includes:

- **type** *(string, required)*: Logical record category. Use `job` when creating downstream idempotency keys and normalized schemas.
- **id** *(string, required)*: France Travail listing identifier.
- **url** *(string, required)*: Canonical listing URL.

Recommended idempotency key: `type + ":" + id`

Use this key for deduplication and upserts so the same listing discovered across repeated runs or overlapping searches resolves to one stable downstream record.

### 6.3 Examples

Example: job (`type = "job"`)

```
{
  "type": "job",
  "id": "206TTWG",
  "url": "https://candidat.francetravail.fr/offres/recherche/detail/206TTWG",
  "title": "Offre n° 206TTWG DIRECTEUR DE MAGASIN H/F - PARIS 8 (H/F)",
  "seedId": "ef38c2d88459",
  "seedType": "query",
  "seedValue": "manager",
  "pageIndex": 4,
  "company": "SRECRUTEMENT",
  "location": "75 - Paris 8e Arrondissement",
  "postalCode": "75008",
  "addressLocality": "Paris",
  "addressRegion": "Île-de-France",
  "addressCountry": "France",
  "mapUrl": "https://fr.mappy.com/plan#/75008%20paris%20e%20arrondissement#xtor=CS1-84-[francetravail]-[lieu-travail]",
  "contractType": "CDI Contrat travail",
  "publishedAt": "2026-04-13T00:00:00",
  "validThrough": "2027-04-13T00:00:00",
  "description": "DIRECTEUR DE MAGASIN Au sein d'une enseigne spécialisée dans le bien-être animal en pleine expansion nous recherchons un Directeur ou une Directrice de Magasin pour notre point de vente à Paris 8. Vous intégrez une structure à taille humaine (600 collaborateurs) qui place la cohésion d'équipe et la proximité client au coeur de son modèle, avec de réelles perspectives d'évolution. Votre quotidien : Piloter et suivre la performance globale du magasin. Animer et manager une équipe motivée et passionnée. Élaborer et suivre le budget du magasin. Appliquer la politique commerciale et sociale de l'enseigne. Garantir le respect des règles d'hygiène et de sécurité. Votre profil ( en plus d'aimer les animaux :) Expérience de 3 ans minimum en management dans le commerce spécialisé, idéalement en ayant touché un peu à l'animalerie. Maîtrise de l'analyse et de la gestion des KPI (compte d'exploitation, fidélisation client, NPS). Compétences en merchandising, gestion et rotation des stocks. Sens du collectif, goût pour les chiffres et force de proposition. Nous ne pourrons considérer votre candidature si pas d'expérience en commerce spécialisé ( uniquement grande distribution par exemple) Les avantages Statut cadre, forfait jour. 11 RTT. Tickets restaurant EDENRED. Mutuelle d'entreprise. Remise salarié sur les produits en magasin. 1% patronal pour les projets de logement et de travaux. Primes valorisant l'engagement et les compétences. Vous vous reconnaissez dans ce descriptif ? Nous avons hâte de recevoir votre candidature ! avec votre CV marketé ( résultats obtenus, kpis utilisés, etc).",
  "salary": 32000,
  "salaryCurrency": "EUR",
  "salaryMin": 32000,
  "salaryMax": 34000,
  "salaryUnit": "YEAR",
  "salaryText": "Salaire brut : Annuel de 32000.0 Euros à 34000.0 Euros sur 12.0 mois Intéressement / participation Titres restaurant / Prime de panier",
  "employmentType": "FULL_TIME",
  "workHours": "39H/semaine Travail en journée Travail le samedi",
  "experienceRequirements": [
    "2 An(s)"
  ],
  "skills": [
    "Assurer le suivi des stocks en temps réel",
    "Présenter et valoriser un produit ou un service",
    "Analyser les tendances de vente pour ajuster les commandes",
    "Diriger et gérer un ensemble, une structure, une organisation",
    "Définir des besoins en approvisionnement",
    "Elaborer une stratégie commerciale",
    "Elaborer, suivre et piloter un budget",
    "Evaluer régulièrement les compétences techniques de l'équipe",
    "Former les nouveaux employés aux techniques de vente",
    "Gérer les retours des clients pour améliorer les services",
    "Identifier et gérer des invendus",
    "Mettre en place des indicateurs de performance technique",
    "Mettre en place une politique de gestion des stocks",
    "Organiser le traitement des commandes",
    "Surveiller régulièrement les performances de vente et ajuster les stratégies",
    "Traiter les réclamations des clients"
  ],
  "softSkills": [
    "Faire preuve de leadership",
    "Faire preuve de rigueur et de précision",
    "Etre force de proposition"
  ],
  "additionalInformation": [
    "Qualification : Cadre",
    "Secteur d'activité : Activités des agences de placement de main-d'œuvre"
  ],
  "companySize": "M. SRECRUTEMENT SRECRUTEMENT",
  "recruiterName": "M. SRECRUTEMENT SRECRUTEMENT",
  "recruiterDescription": "Voir la page employeur",
  "employerPageUrl": "https://recrute.francetravail.fr/page-employeur/ronat-sylvain-113",
  "employerPhone": "0668786396",
  "applyActionUrl": "https://candidat.francetravail.fr/offres/recherche.rechercheoffre.voletdetail.postuler.contact:chargercontact?emission=1&idOffre=206TTWG&indexFin=80&lieux=75D&motsCles=manager&offresPartenaires=true&range=60-79&rayon=10&tri=0",
  "contactActionUrl": "https://candidat.francetravail.fr/offres/recherche.rechercheoffre.voletdetail.postuler.contact:chargercontact?emission=1&idOffre=206TTWG&indexFin=80&lieux=75D&motsCles=manager&offresPartenaires=true&range=60-79&rayon=10&tri=0",
  "industry": "Activités des agences de placement de main-d'œuvre",
  "qualification": "Cadre"
}
```

## Field reference

### Job fields (`type = "job"`)

- **type** *(string, required)*: Logical record category for downstream normalization.
- **id** *(string, required)*: France Travail listing identifier.
- **url** *(string, required)*: Canonical listing URL.
- **title** *(string, required)*: Listing title as shown on France Travail.
- **seedId** *(string, required)*: Stable identifier for the originating search input.
- **seedType** *(string, required)*: Origin of the search input, such as a query-based run.
- **seedValue** *(string, required)*: Original query or source value that produced the record.
- **pageIndex** *(integer, required)*: Source results page index for the record.
- **company** *(string, optional)*: Employer or hiring company name.
- **location** *(string, optional)*: Human-readable job location.
- **postalCode** *(string, optional)*: Postal code when available.
- **addressLocality** *(string, optional)*: City or locality.
- **addressRegion** *(string, optional)*: Region name.
- **addressCountry** *(string, optional)*: Country name.
- **mapUrl** *(string, optional)*: Public map link associated with the job location.
- **contractType** *(string, optional)*: Contract type text shown on the listing.
- **workTime** *(string, optional)*: Working time label, such as full-time or part-time.
- **publishedAt** *(string, optional)*: Publication timestamp.
- **validThrough** *(string, optional)*: Expiration or validity timestamp when provided.
- **description** *(string, optional)*: Full job description text.
- **salary** *(number, optional)*: Convenience salary value when provided.
- **salaryCurrency** *(string, optional)*: Salary currency code.
- **salaryMin** *(number, optional)*: Lower bound of the salary range.
- **salaryMax** *(number, optional)*: Upper bound of the salary range.
- **salaryUnit** *(string, optional)*: Salary period, such as year or month.
- **salaryText** *(string, optional)*: Original salary text as displayed.
- **employmentType** *(string, optional)*: Employment type value such as full time.
- **workHours** *(string, optional)*: Working hours or schedule text.
- **experienceRequirements** *(array[string], optional)*: Experience requirements listed on the job.
- **skills** *(array[string], optional)*: Skill requirements or competencies.
- **softSkills** *(array[string], optional)*: Behavioral or soft-skill requirements.
- **additionalInformation** *(array[string], optional)*: Additional listing details not represented in dedicated fields.
- **companySize** *(string, optional)*: Employer size or employer label shown on the listing.
- **recruiterName** *(string, optional)*: Recruiter or employer contact name.
- **recruiterDescription** *(string, optional)*: Recruiter summary text.
- **employerPageUrl** *(string, optional)*: Public employer page URL when available.
- **employerLogoUrl** *(string, optional)*: Public employer logo URL when available.
- **employerPhone** *(string, optional)*: Public phone number when available.
- **employerEmail** *(string, optional)*: Public email address when available.
- **applyActionUrl** *(string, optional)*: Public application URL shown with the listing.
- **contactActionUrl** *(string, optional)*: Public contact URL shown with the listing.
- **industry** *(string, optional)*: Employer industry or activity sector.
- **qualification** *(string, optional)*: Qualification level shown on the listing.
- **jobLabels** *(array[string], optional)*: Additional listing labels or tags when available.

## Data guarantees & handling

- **Best-effort extraction:** fields may vary by region, session, availability, and UI experiments.
- **Optional fields:** null-check in downstream code.
- **Deduplication:** recommend `type + ":" + id`.

## How to Run on Apify

1. Open the Actor in Apify Console.
2. Configure your search parameters, such as keywords, location, publication recency, contract type, or job category.
3. Set the maximum number of outputs to collect with the `limit` field.
4. Click **Start** and wait for the run to finish.
5. Download results in JSON, CSV, Excel, or other supported formats.

## Scheduling & Automation

### Scheduling

**Automated Data Collection**

You can schedule recurring runs to keep your France Travail job dataset fresh without starting each run manually. This is useful for monitoring hiring activity, building rolling dashboards, or keeping enrichment workflows up to date.

- Navigate to **Schedules** in Apify Console
- Create a new schedule (daily, weekly, or custom cron)
- Configure input parameters
- Enable notifications for run completion
- Optional: add webhooks for automated processing

### Integration Options

- **Webhooks:** Trigger downstream actions when a run completes
- **Zapier:** Connect to 5,000+ apps without coding
- **Make (Integromat):** Build multi-step automation workflows
- **Google Sheets:** Export results to a spreadsheet
- **Slack/Discord:** Receive notifications and summaries
- **Email:** Send automated reports via email

## Performance

- **Small runs (< 1,000 outputs):** ~2-3 minutes
- **Medium runs (1,000-5,000 outputs):** ~5-15 minutes
- **Large runs (5,000+ outputs):** ~15-30 minutes

Execution time varies based on filters, result volume, and how much information is returned per record.

## Compliance & Ethics

### Responsible Data Collection

This actor collects publicly available job posting information from [https://francetravail.fr](https://francetravail.fr) for legitimate business purposes. Common use cases include labor market research and market analysis, recruiting intelligence and benchmarking, and job monitoring or reporting workflows. Users are responsible for ensuring their collection, storage, and use of data complies with applicable laws, regulations, and platform terms. This section is informational and not legal advice.

- **Labor market** research and market analysis
- **Recruiting intelligence** and benchmarking
- **Job monitoring** and reporting workflows

### Best Practices

- Use collected data in accordance with applicable laws, regulations, and the target site's terms
- Respect individual privacy and personal information
- Use data responsibly and avoid disruptive or excessive collection
- Do not use this actor for spamming, harassment, or other harmful purposes
- Follow relevant data protection requirements where applicable (e.g., GDPR, CCPA)

## Support

For help, use the Issues tab or the actor page on Apify and include the input you used with sensitive values redacted, the run ID, a short description of expected versus actual behavior, and an optional small output sample that shows the problem clearly.