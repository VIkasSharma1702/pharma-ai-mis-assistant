# 📊 AI-Powered MIS Assistant

> **Enterprise-Grade Conversational Analytics Engine for Pharma Sales Teams**  
> *Built specifically to empower sales reps and managers, eliminating manual Excel filtering and pivot table dependencies.*

---

## 📌 Overview

An intelligent, cloud-based Management Information System (MIS) Assistant tailored for the pharmaceutical distribution industry. Built entirely on the **Google Workspace ecosystem (Apps Script)** and powered by **Google Gemini 2.5 Flash**, this tool transforms heavy, static spreadsheets (80,000+ rows) into a blazing-fast conversational data engine.

Sales representatives and field managers can interact with their live data using natural language (English/Hinglish) to generate instant performance insights, complex pivot tables, and dynamic downloadable reports—all from their mobile or laptop within seconds.

---

## 🔄 The Data Pipeline

👤 **Sales Rep Prompt** (Hinglish/English)  
&nbsp;&nbsp; ↳ 🧠 **Gemini LLM** (Parses unstructured text into strict JSON intent)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↳ ⚡ **GZIP Cache Layer** (Decompresses 80k+ rows into memory instantly)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↳ ⚙️ **V8 Query Engine** (Filters, groups, and pivots data in a single pass)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ↳ 📊 **Output Delivery** (Client-side CSV Blob / Chat UI response)

---

## ✨ Key Features & Capabilities

| Feature | Technical Description |
| :--- | :--- |
| **🧠 NLP & Entity Alignment** | Understands conversational Hinglish. Uses Gemini to map shorthand or misspelled words to the exact database entries (e.g., auto-correcting typos to strict uppercase database values) via dynamic validation lists. |
| **⚡ Chunked GZIP Caching** | Solves Apps Script's 100KB cache limit by packing, compressing, and splitting 80,000+ transactional rows into multiple ~90KB Base64 chunks for sub-6-second reads. |
| **📉 Missed Orders Engine** | Features a mathematical churn tracker. Compares distinct buyers from the previous month against the current month to instantly flag inactive accounts for sales follow-ups. |
| **📊 Dynamic Excel Pivot** | Bypasses manual Excel work by generating automated Month-vs-Party cross-tabs. Missing ordering periods dynamically render as `0` sales. |
| **📥 Token-Optimized Export** | Prevents LLM Rate Limits (HTTP 429) by bypassing secondary text-generation when exporting large datasets. Generates pure Client-Side CSV Blobs instantly. |

---

## 💬 Live Query Examples (For Sales Team)

This assistant doesn't just answer questions; it understands complex field sales logic. Here is how the sales team can interact with it:

* **Sales Rep Performance:** *" [Salesman Name] ki total sales kitni hui hai?"*
* **Multi-Value Filtering:** *"[Salesman A] aur [Salesman B] ki item-wise sale download karo."*
* **Instant Inventory Access:** *"[Product Name] ka live stock status check karo order lene se pehle."*
* **Advanced Pivot/Cross-Tab:** *"April, May, June me kis party ne order diya aur kisne nahi diya, excel me do."*
* **Lead Revival (Churn):** *"Kis party ne pichle mahine order diya par is mahine unka koi order nahi aaya?"*

---

## 🛠️ Tech Stack

| Component | Technology Used |
| :--- | :--- |
| **AI Core (LLM)** | Google Gemini 2.5 Flash API (Structured JSON Responses) |
| **Backend / Runtime** | Google Apps Script (V8 Engine) |
| **Database** | Google Sheets (Relational Ledger) |
| **Caching Mechanism** | Custom Utilities GZIP + Apps Script `CacheService` |
| **Frontend UI** | HTML5, CSS3, ES6 JavaScript, Asynchronous `google.script.run` |

---

## 📂 Architecture Under the Hood

* **`Config.gs`:** Master configuration. Holds spreadsheet IDs, active models, and column headers (`FIELD_MAP` & `STOCK_FIELD_MAP`).
* **`Cache.gs`:** The backbone of performance. Handles data pulling, text-date fallback parsing, GZIP compression, and multi-chunk Base64 distribution.
* **`QueryEngine.gs`:** The analytics powerhouse. Contains independent, single-pass evaluation loops for standard filtering, multi-array OR matching, and delta logic (`runMissedOrdersQuery_`).
* **`AIEngine.gs`:** Bridges the app with the Generative Language API. Manages system prompts, few-shot examples, JSON schema enforcement, and intelligent rate-limit bypassing.
* **`Index.html`:** A lightweight, dark-mode single-page application (SPA). Manages UI state, loading hooks, and compiles binary blobs into downloadable CSVs without server-side file creation.

---

## 📈 Business Impact for Sales Teams

✅ **Zero Pivot Tables Needed** — Fully automated data extraction saves hours of daily manual Excel formatting for managers and field reps.  
✅ **Lightning Fast Execution** — Queries against 80,000+ rows return results in `<6 seconds` while agents are live on the field.  
✅ **Proactive Client Retention** — Sales teams get instant access to churned clients (Missed Orders), accelerating follow-up calls and recovering lost revenue.  
✅ **Data Independence** — Field staff no longer need to call the back-office or wait for MIS operators to get custom reports. They just ask the AI and download the data sheet instantly.
