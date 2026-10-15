<div align="center">
  <img src="https://img.shields.io/badge/Status-Proprietary_Software-red?style=for-the-badge" alt="Proprietary Software">
  <img src="https://img.shields.io/badge/Available_For-Freelance_Hire-blue?style=for-the-badge" alt="Available for Freelance Hire">
</div>

<br>

# B2B Lead Intelligence & AI Enrichment Engine

An end-to-end lead research pipeline that transforms local business listings into enriched, evidence-backed prospect data for outbound campaigns.

Instead of delivering a basic directory export, the system combines official business discovery, live website research, technical footprint analysis, AI enrichment, deterministic scoring, and human review into a clean CRM-ready CSV.

> **Proprietary software:** this public repository is a product and engineering case study. The application source code, scraping pipeline, prompts, validation rules, and operational data remain private.

---

## Application Preview

From search configuration and reusable batch history to evidence-backed enrichment and human review:

### Search and saved batches

![B2B Lead Machine search interface with AI enrichment and saved searches](assets/lead-search-interface.png)

### Enriched lead review

![Enriched lead with quality score, Meta Pixel detection, business intelligence, evidence-backed icebreakers, and review controls](assets/lead-results-dashboard.png)

---

## The Problem

Raw business listings rarely contain enough context for effective outreach. Sales teams still need to visit websites, locate public contact information, understand each company's positioning, identify relevant sales angles, and manually clean the resulting spreadsheet.

This project automates that research workflow while keeping uncertain information explicit instead of inventing missing facts.

## What the System Does

1. **Targeted business discovery**
   - Searches by niche, city, and geographic intent through the Google Places API.
   - Normalizes business names, addresses, phone numbers, websites, ratings, and review counts.
   - Deduplicates results before enrichment.

2. **Multi-page website research**
   - Uses asynchronous Playwright browsers to execute JavaScript and inspect live pages.
   - Discovers relevant pages such as Home, About, Services, and Contact.
   - Extracts visible website content and preserves source URLs for auditing.

3. **Public contact and email intelligence**
   - Finds publicly listed business emails and records where they were found.
   - Prioritizes domain-matching addresses and classifies lower-quality or generic candidates.
   - Keeps missing contact data clearly marked instead of filling it with guesses.

4. **Technical footprint audit**
   - Detects Meta Pixel signals after client-side JavaScript execution.
   - Converts technical findings into readable statuses rather than ambiguous `Yes/No` fields.

5. **Evidence-backed AI enrichment**
   - Uses Gemini with a structured JSON response contract.
   - Generates an exact niche classification, executive summary, target audience, core services, and up to three personalized outreach icebreakers.
   - Cross-checks generated claims against text collected from the company's website.
   - Returns `insufficient_evidence` when the available content cannot support a reliable conclusion.

6. **Lead scoring and human review**
   - Assigns a deterministic 0–100 quality score and an A/B/C grade.
   - Supports review states for approval, revision, or rejection.
   - Allows operators to refine outreach copy before final delivery.

7. **Batch operations and delivery**
   - Runs background collection jobs with live progress and cancellation support.
   - Saves previous searches locally so results can be reopened without repeating API calls.
   - Exports all leads or only approved leads to a clean CSV for CRM and outreach tools.

---

## Example Deliverable

| Data group | Example fields |
|---|---|
| Business identity | Company name, address, phone, website, rating, review count |
| Contact intelligence | Public email, email quality, email source URL |
| Technical audit | Meta Pixel detection status |
| AI intelligence | Exact niche, executive summary, target audience, core services |
| Outreach personalization | Up to three evidence-backed icebreakers with source references |
| Quality control | Lead score, A/B/C grade, review status |

The commercial deliverable is a curated CSV dataset. The automation itself is not distributed as part of the standard service.

---

## Architecture

```text
Search criteria
      ↓
Google Places discovery and deduplication
      ↓
Async website navigation and page discovery
      ↓
Contact extraction and technical audit
      ↓
Structured AI enrichment and evidence validation
      ↓
Deterministic scoring and human review
      ↓
CRM-ready CSV export
```

### Technology Stack

- **Backend:** Python 3.12, FastAPI, Pydantic
- **Browser automation:** Playwright Async with bounded concurrency
- **Data source:** Google Places API (New)
- **AI enrichment:** Gemini API with structured JSON output
- **Persistence:** SQLite with WAL mode
- **Frontend:** HTML, Tailwind CSS, Vanilla JavaScript
- **Testing:** Pytest-based pipeline and validation tests

### Engineering Highlights

- Blocking SDK operations are isolated from FastAPI's event loop.
- Browser concurrency is limited to protect memory and system stability.
- Website evidence is collected once and reused across enrichment and validation steps.
- AI output must conform to a defined schema and pass local evidence checks.
- Partial progress is persisted, reducing data loss during long-running jobs.
- Review status is stored separately from the lead payload for safer curation.
- CSV output is formatted for reliable opening in spreadsheet and outreach applications.

---

## Reliability Boundaries

- Results depend on Google Places coverage for the requested query and location.
- Only publicly available website information is collected.
- An email can be publicly sourced and syntactically valid without guaranteeing mailbox deliverability.
- Some websites block automated browsers or expose too little content for AI enrichment.
- Unsupported claims are rejected or marked as insufficient evidence.
- The current product is an operator-assisted service, not a public multi-tenant SaaS platform.

---

## Ideal Use Cases

- B2B marketing and cold email agencies
- Founders and sales teams targeting local service businesses
- Custom market research and prospect-list projects
- Campaigns that require personalized, evidence-backed outreach angles
- Technical audits for businesses missing important marketing instrumentation

---

## Work With Me

I build custom data extraction, browser automation, lead intelligence, and API integration solutions. Engagements can range from a focused test batch to a custom multi-location research campaign.

- **Upwork:** [Hire me on Upwork](https://www.upwork.com/freelancers/~01863b330a3897a766?mp_source=share)
- **Contra:** [View my Contra portfolio](https://contra.com/kauan_miranda_1uvmpwxm?referralExperimentNid=DEFAULT_REFERRAL_PROGRAM&referrerUsername=kauan_miranda_1uvmpwxm)
