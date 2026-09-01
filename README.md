# 🚀 B2B Lead Machine (Proprietary Architecture)

A high-performance, asynchronous B2B Lead Generation engine designed to automate local business prospecting for marketing agencies. It eliminates manual Google Maps searches, parses contact emails, and detects active Facebook Pixels at scale using a highly optimized, resource-safe browser pipeline.

> 🔒 **Proprietary Software Notice:** The backend scraping infrastructure, concurrent browser orchestrator, and source code are closed-source to protect intellectual property. It is displayed here as a case study in high-performance web automation.

---

## 🎥 Video Demonstration
<img width="1138" height="738" alt="Decolar gif reduzido" src="https://github.com/user-attachments/assets/248e323e-5acd-4171-9d5f-44b0586e3b51" />

---

## 📸 Software Preview
<img width="1153" height="758" alt="Image" src="https://github.com/user-attachments/assets/f113b62b-1300-4f7e-810f-aa2aeac60ed8" />

---

## 🛠️ Tech Stack & Engineering

### 🟢 Core Technologies
* **Backend Framework:** FastAPI (Python 3.12) - High-performance asynchronous ASGI server.
* **Web Automation:** Async Playwright (Headless Chromium Orchestration).
* **Data Sourcing:** Google Places API (Places & Details Endpoints).
* **Data Parsing:** Native Python `re` (Asynchronous Regex Engine for Email Extraction).
* **Frontend UI:** Tailwind CSS, Vanilla JavaScript (Asynchronous Fetch API).

### 📐 Engineering Highlights & Architecture

To scale this application from a local script to an enterprise-grade microservice, the system was completely refactored around non-blocking asynchronous principles:

1. **Non-Blocking Thread Isolation (`asyncio.to_thread`)**
   The Google Places API wrapper relies on synchronous HTTP requests. To prevent these blocking networking calls from freezing the FastAPI main event loop (which would make the server unresponsive to other users), all Google Maps API operations are isolated and delegated to separate OS threads using `asyncio.to_thread`.

2. **Memory-Safe Concurrency Control (`asyncio.Semaphore`)**
   Running headless browsers (Chromium) is highly resource-intensive, consuming roughly 150MB-300MB of RAM per active tab. To prevent server crashes due to Out-Of-Memory (OOM) errors in resource-constrained environments (such as a standard 1GB VPS cloud instance), the pipeline implements a strict execution concurrency guard using `asyncio.Semaphore(3)`. This limits the worker to a maximum of 3 concurrent browser instances, queueing extra requests safely.

3. **Active Polling vs. Static Sleep (`wait_for_function`)**
   Instead of using brittle, static timeouts (like forcing the browser to sleep for 3-5 seconds to wait for scripts to load), the automation engine actively polls the DOM. It checks for the existence of the `window.fbq` object (Facebook Pixel) with a hard dynamic limit of `3000ms`. If the Pixel is detected in 100ms, the worker continues instantly. If the site has no Pixel, it catches the timeout exception safely and moves on, boosting batch processing speeds up to 10x.

---

## 🚀 Key Features Demonstrated
* **Automated Lead Extraction:** Instant harvesting of localized businesses via Google Places API.
* **Smart Lead Qualification:** Live, dynamic Facebook Pixel detection (Hot/Cold targeting) via isolated headless web browsers.
* **CRM-Ready Export:** One-click CSV formatting designed specifically for seamless import into HubSpot, Salesforce, or GoHighLevel.

---

## 💼 Business Inquiries
Need a custom, highly scalable data extraction pipeline or lead-generation solution for your marketing agency? Let's build yours.

* 🔗 **Upwork:** [Hire me on Upwork](https://www.upwork.com/freelancers/~01863b330a3897a766?mp_source=share)
* 🔗 **Contra:** [View my Contra Portfolio](https://contra.com/kauan_miranda_1uvmpwxm?referralExperimentNid=DEFAULT_REFERRAL_PROGRAM&referrerUsername=kauan_miranda_1uvmpwxm)
