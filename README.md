# AI-Powered MIS Assistant (Pharma Sales & Inventory Engine)

An intelligent, conversational Management Information System (MIS) Assistant tailored for the pharmaceutical distribution industry. Built on top of **Google Apps Script** and powered by **Gemini 2.5 Flash**, this tool transforms flat spreadsheets (80,000+ rows) into a blazing-fast, secure, conversational data analytics engine that processes natural language queries (English/Hinglish) and automatically generates dynamic downloadable Excel reports.

---

## 🚀 Key Features

### 1. Conversational Data Interface
* Fully understands text prompts in English, Hindi, and Hinglish.
* Dynamically parses user intent into strict query schemas using Gemini's structured JSON outputs.
* Automatically aligns misspelled or shorthand names (e.g., matching "nandini" to `NANDANI (SALES)`) by validating inputs against live datasets.

### 2. High-Performance Caching Layer (`~6-second execution`)
* Implements a **custom chunked GZIP compression layer** inside Google Script's `CacheService`.
* Packs, compresses, and splits over 80,000 rows of transactional sales data into ~90KB Base64 string chunks to completely bypass Apps Script quotas and provide instantaneous query execution.

### 3. Dynamic Excel/CSV Export Engine
* Detects when a user asks for spreadsheet files (e.g., *"excel me do"*, *"download report"*).
* Bypasses secondary generative LLM formatting when exporting heavy files to conserve API tokens and avoid Rate Limit errors (HTTP 429).
* Instantly generates client-side CSV downloads for detailed sales, dynamic pivots, or inventory arrays.

### 4. Advanced Pharma Analytics
* **Automatic Pivot Tables (Cross-tabs):** Handles complex matrix queries like *"April, May, June me kisne order diya aur kisne nahi"* by structuring a `Party vs Month` dataset where missing ordering periods dynamically render as zero sales.
* **Multi-Value Filtering:** Supports compound filtering (e.g., tracking multiple salesmen simultaneously like *"Rimpi, Anmol, Ritika, and Nandini"*), dynamically parsing the string list into internal programmatic `OR` evaluation flags.
* **Missed Orders Tracker:** Runs mathematical delta audits comparing distinct ordering entities from the previous calendar month against active entries in the current month to flag inactive accounts for sales follow-ups.

### 5. Security & Privacy Firewall (Zero Price Leakage)
* Designed with high-security boundaries for warehouse/public querying.
* The caching engine applies a **strict field-level block** on the `stock` sheet. It only extracts `Product Name`, `Company`, and `Current Stock` from Row 4 onwards (Row 3 headers), completely ignoring confidential fields like Cost Price, Purchase Rates, Sales Margins, and Total Stock Values.

---

## 🛠️ Tech Stack

* **Backend / Database Layer:** Google Sheets + Google Apps Script (GAS)
* **AI Core:** Google Gemini 2.5 Flash API (Structured JSON Responses)
* **Caching:** Utilities GZIP + Google Script CacheService
* **Frontend UI:** Vanilla HTML5, CSS3 (Dark Mode Template), and native Asynchronous Google Script Runners (`google.script.run`)

---

## 📂 File Architecture

* **`Config.gs`:** Main structural routing settings. Houses spreadsheet identifiers, active worksheet names, active model declarations, and explicit string mappings for both Sales (`FIELD_MAP`) and Stock (`STOCK_FIELD_MAP`) headers.
* **`Cache.gs`:** Handles raw spreadsheet read actions, data cleaning, string date formatting parsing fallbacks, GZIP stream encoding, and multi-chunk cache generation routines.
* **`QueryEngine.gs`:** The analytics powerhouse containing independent, single-pass evaluation logic for standard transactional parsing, multiple array match filters, stock auditing, and date gap comparisons (`runMissedOrdersQuery_`).
* **`AIEngine.gs`:** Interfaces with the Generative Language API. Manages system prompts, few-shot prompt alignments, response mime schemas, API error bypass rules, and natural text output generators.
* **`Index.html`:** Lightweight single-page dashboard. Houses styling variables, message state rendering handlers, input hooks, and client-side binary blob compilation logic for automatic report generation.

---

## ⚙️ Setup and Installation

### 1. Sheet Structure Setup
Ensure your Google Spreadsheet contains two core sheets:
* **Sales Sheet (`Sheet1`):** Row 1 must contain strict sales header properties matching your `FIELD_MAP` declarations (e.g., `Party Name`, `Item Name`, `Amount`, etc.).
* **Stock Sheet (`stock`):** Row 3 must contain your explicit inventory headers (`Product Name`, `Company`, `Current Stock`). Data must strictly begin from Row 4 downwards.

### 2. Apps Script Integration
1. Inside your Google Sheet, navigate to **Extensions > Apps Script**.
2. Delete any existing code and create the 5 distinct files matching the architecture (`Config.gs`, `Cache.gs`, etc.).
3. Copy the corresponding repository scripts into each file.

### 3. API Environment Variables
1. In the Apps Script Editor, click on the **Project Settings (Gear Icon)**.
2. Scroll to **Script Properties** and click **Add script property**.
3. Set the Property key as `GEMINI_API_KEY` and paste your secret token generated from [Google AI Studio](https://aistudio.google.com/).

### 4. Initialize Data Cache
1. Open `Cache.gs` in the editor.
2. Select the `refreshCache` function from the top toolbar dropdown.
3. Click **Run (▶)** and authorize required sheet/external request permissions. Check the Execution Log to ensure all sales and stock rows are cleanly cached.
4. *(Optional)* Run the `setupTrigger` function once to automatically recalculate and synchronize the local dataset cache every 5 hours.

### 5. Web App Deployment
1. Click **Deploy > New deployment** in the upper right.
2. Select **Web app** as the deployment type.
3. Set *Execute as* to **Me**, and *Who has access* to **Anyone** (or your preferred team restriction).
4. Click **Deploy**, copy the provided URL, and paste it into any web browser to access your conversational MIS dashboard!

---

## 📝 Query Examples to Try

* **Sales Lookup:** *"Nandani ki total sales kitni hai"*
* **Complex Cross-Tab Pivot:** *"April May June me kis party ne order diya aur kisne nahi diya excel me"*
* **Targeted Multi-Filter Sheet:** *"Rimpi aur Anmol ki july ki item wise sale download karo"*
* **Secure Stock Search:** *"Paracetamol ka live stock status check karo"*
* **Churn Analytics Report:** *"Kis party ne pichle mahine order diya par is mahine unka koi order nahi aaya"*
