# Tools & Workflows Reference

A reference for AI assistants and collaborators. Describes every active repository, tool, pipeline, and deployment so full context doesn't need to be re-gathered each time.

**Author:** Austin Smith ([@Leerrooy95](https://github.com/Leerrooy95))
**Last Updated:** March 31, 2026

---

## Live Deployments

| Service | URL | Hosted On | Source Repo |
|---------|-----|-----------|-------------|
| Live Intelligence Dashboard | [regulatedfriction.me](https://regulatedfriction.me) | GitHub Pages (Live_Trackers, private) | — |
| Gradient AI Chatbot | Embedded on regulatedfriction.me | Gradient AI (DigitalOcean) | — |
| Federal Register Scraper | Automated | DigitalOcean | Private |
| DOJ Press Release Scraper | Automated | DigitalOcean | Private |
| Portfolio Website | [leerrooy95.github.io](https://leerrooy95.github.io) | GitHub Pages | [leerrooy95.github.io](https://github.com/Leerrooy95/leerrooy95.github.io) |
| OSINT ChatBot | [personal-chatbot-qej0.onrender.com](https://personal-chatbot-qej0.onrender.com/login) | Render (free tier) | [OSINT_ChatBot](https://github.com/Leerrooy95/OSINT_ChatBot) |
| Bill Translator | [bill-translator.onrender.com](https://bill-translator.onrender.com/) | Render (free tier) | [Bill_Translator](https://github.com/Leerrooy95/Bill_Translator) |

---

## Active Repositories

### 1. The Regulated Friction Project (v11.3)

**Purpose:** Research-only information repository. Documents temporal correlations between geopolitical friction events and institutional capital flows (2015–2026).

**Key contents:**
- 16-section research corpus (00_Quick_Breakdowns through 15_The_Religious_Layer)
- `_AI_CONTEXT_INDEX/` — 12 structured markdown files + Node Dossiers (14 active leverage nodes) used by AI assistants and the OSINT ChatBot
- `15_The_Religious_Layer/` — Religious infrastructure mapping (Paula White, Capitol Ministries, CUFI/Hagee, CREC/Wilson, Hegseth convergence node)
- `10_Real-Time_Updates_and_Tasks/2026_March/` — April 2026 convergence window prediction, Cuba crisis escalation, Mueller death/leverage signal, Musk empire realignment, AI kill chain / Minab school strike analysis
- `Project_Trident/` — independent verification suite (16 statistical tests by Opus 4.6)
- `Run_Correlations_Yourself/` — reproducibility scripts
- `output/` — daily data synced from Live_Trackers pipeline

**Workflows:**
- `sync_from_live_trackers.yml` — pulls latest pipeline output from Live_Trackers daily at 10:00 UTC

**Core statistics:** r = +0.6196 (p = 0.0004), 66 verified event pairs, 7-day median lag

**Active leverage nodes (14):** Maxwell, Iran, Gulf SWFs, Israel, Epstein Files, Oracle/Ellison, Arkansas Datacenter, Religious Layer, April 2026 Convergence Window, Zorro Ranch/NM Investigation, Cuba Crisis, Musk/SpaceX-xAI Empire Realignment, AI Kill Chain/Minab School Strike, Capital Architecture (USD1/WLF/MGX)

**Note:** The Streamlit dashboard has been retired. All live monitoring is in Live_Trackers (now private). Deprecated files (Streamlit source, Scrapy spider, old workflows) are in `Archive/`.

---

### 2. Live_Trackers (v2.4) — **Private Repository**

**Purpose:** Unified real-time intelligence pipeline powering the live dashboard at regulatedfriction.me.

**Seven-stage pipeline:**

| Stage | Script | AI Model | Function |
|-------|--------|----------|----------|
| 1 | `node_tracker.py` | Brave Search + Anthropic Claude | Queries current status of leverage nodes via web search, classifies events with LLM analysis. Includes regulatory capture and revolving door detection. |
| 2 | `entity_extractor.py` | GLiNER2 (local) + Llama Scout 17B (API) | Dual-engine entity extraction and relation mapping. GLiNER2 runs zero-cost on CPU; Llama Scout fills gaps when key is set. Results merged with cross-node connection detection. |
| 2.5 | `graph_builder.py` | Local (no API) | Reads extracted_entities.json, builds NetworkX graph, renders interactive PyVis HTML visualization to docs/data/entity_graph.html |
| 3 | `convergence_detector.py` | Local (no API) | Detects multi-node convergence patterns from historical runs |
| 3.5 | `chart_data_builder.py` | Local (no API) | Aggregates historical run data into chart_data.json |
| 4 | `daily_intelligence.py` | Brave Search + Anthropic Claude | Three-pass investigation protocol (signal sweep, cross-node scan, under-radar probe). Tracks signals, breaking news, prediction verification. |
| 5 | `fact_checker.py` | Brave Search + Anthropic Claude | Web-grounded fact verification — searches Brave for live evidence, then Claude verifies claims against both web results and training knowledge. Corrects errors in-place. |
| 6 | `rhetoric_reality.py` | Anthropic Claude | Three-column gap analysis (rhetoric vs. reality) with statute citations |

**GLiNER2 details:**
- Model: `fastino/gliner2-base-v1` (205M parameters, Apache 2.0)
- Runs locally on GitHub Actions CPU runner — zero API cost
- Extracts entity types: person, organization, jurisdiction, capital_flow, date, policy, crypto_asset, leverage_node
- Performs relation extraction: ownership, investment, conflict, leadership, administrative control, personal guarantee, mediation
- Zero-cost fallback mode: when `LLAMA_SCOUT_KEY` is not set, pipeline runs GLiNER2-only automatically
- New CLI flag: `--gliner-only` to force local extraction
- Cross-node connection detection: automatically identifies shared entities across leverage nodes

**Leverage nodes tracked:** Maxwell, Iran, Gulf SWFs, Israel, Oracle/Ellison, Epstein Files, Arkansas Datacenter, Religious Layer, Zorro Ranch/NM, April 2026 Window, Cuba Crisis, Capital Architecture (USD1/WLF/MGX), Musk/SpaceX-xAI Empire Realignment, AI Kill Chain/Minab School Strike

**Output:** JSON files in `output/` — node_status, extracted_entities, convergence_report, daily_intelligence, live_verification, fact_check, rhetoric_reality, chart_data. Timestamped copies in `output/history/`. Entity graph rendered to `docs/data/entity_graph.html`.

**Dashboard:** Nine-tab static HTML/CSS/JS at regulatedfriction.me (**Node Status**, **Intelligence**, **Convergence**, **Predictions**, **Entities**, **Entity Graph**, **Charts**, **Rhetoric vs. Reality**, **History**). Chart.js visualizations: Thermostat Timeline, Dual-Track Stacked Area, Node Activation Heatmap. Interactive entity relationship graph (NetworkX + PyVis): color-coded by entity type (red=leverage nodes, blue=persons, green=organizations, yellow=locations, purple=financial, orange=legal), sized by connection frequency, dashed yellow convergence edges for cross-node connections. Prediction Tracker displays confirmed and failed predictions publicly. Embedded Gradient AI chatbot with `_AI_CONTEXT_INDEX` knowledge base.

**Workflows:**
- `run_pipeline.yml` — runs the full seven-stage pipeline twice daily (08:00 / 20:00 UTC), publishes to dashboard
- `deploy.yml` — CI/CD validation on push to main

**API budget:** Node tracker: 50 calls/day. Daily intelligence: 100 calls/day. Llama Scout: 1 call/run (optional). GLiNER2: 0 API calls (local). Convergence: no API calls.

**Required secrets:** `BRAVE_API_KEY`, `ANTHROPIC_API_KEY`
**Optional secrets:** `LLAMA_SCOUT_KEY` (enables dual-engine mode; GLiNER2-only runs automatically without it)

**Dependencies added (March 22, 2026):** `gliner2`, `networkx`, `pyvis` — all verified no security advisories.

**Migration (March 31, 2026):** Perplexity sonar-pro replaced with Brave Search API + Anthropic Claude across Stages 1, 4, and 5. `openai` and `azure-ai-inference` packages removed from requirements. Web-grounded fact verification added to Stage 5. Regulatory capture detection added to node tracker prompts. Daily intelligence API budget increased from 75 to 100.

**Note:** This repository is private. The website and pipeline remain active.

---

### 3. DigitalOcean Infrastructure

**Purpose:** Automated data collection and AI chatbot hosting outside of GitHub Actions.

**Deployed services:**

| Service | Function | Schedule |
|---------|----------|----------|
| Federal Register Scraper | Scrapes Federal Register for regulatory filings, executive orders, and rule changes relevant to tracked nodes | Automated |
| DOJ Press Release Scraper | Scrapes Department of Justice press releases for enforcement actions, indictments, and policy announcements | Automated |
| Gradient AI Chatbot | Chatbot deployed on DigitalOcean with live dashboard context injection — the `_AI_CONTEXT_INDEX` knowledge base is loaded so the chatbot can answer questions about the project's current findings and pipeline outputs | Persistent |

**Note:** Scraper output feeds into the Live_Trackers pipeline. The Gradient AI chatbot is embedded on the regulatedfriction.me dashboard.

---

### 4. Crypto Monitoring Pipeline

**Purpose:** Tracks stablecoin capital flows and regulatory developments related to the USD1/WLF/MGX capital architecture documented in the Regulated Friction Project.

**What it monitors:**
- USD1 stablecoin market cap and transaction volume
- World Liberty Financial (WLF) OCC charter application status
- MGX/Abu Dhabi capital flows through Binance/USD1
- GENIUS Act and CLARITY Act legislative status
- Emoluments Clause concerns (Warren/Merkley)

**Output:** Chart.js visualizations integrated into the live dashboard; pipeline JSON outputs feeding convergence detection.

---

### 5. OSINT_ChatBot

**Purpose:** BYOK (Bring Your Own Key) chat interface powered by Anthropic Claude with a knowledge base from `_AI_CONTEXT_INDEX/`.

**Stack:** Python, Flask, Anthropic Messages API

**How it works:**
1. Knowledge base markdown files are loaded into memory at startup (`knowledge_base.py`)
2. Files are injected into the system prompt on every request
3. Users provide their own Anthropic API key in the browser — stored only in encrypted session cookies, never on disk
4. Claude answers based on: (1) knowledge base, (2) training data, (3) explicit "I don't know"

**Security features:** BYOK model, API key format validation, CSRF protection, rate limiting (10 login/min, 30 chat/min), DOMPurify sanitization, security headers (CSP, HSTS, X-Frame-Options), HttpOnly/SameSite/Secure cookies, 2-hour session expiry

**Deployment:** Render with `render.yaml` blueprint. Only env var: `FLASK_SECRET_KEY` (auto-generated).

---

### 6. Bill_Translator

**Purpose:** Production Flask web application that rewrites dense legal text to meet 8th-grade readability standards while preserving legal intent. Addresses Arkansas Act 602.

**Stack:** Python, Flask, Anthropic API (Claude Sonnet 4), Textstat

**Key features:**
- Built-in Flesch-Kincaid scorer (local, no API needed)
- Meaning drift detection — extracts legal terms before translation, compares after
- Three translation modes: full simplification, preserve legal terms, jargon-only replacement
- Auto re-iteration until target grade reached
- Score-only mode, batch mode
- Web UI with side-by-side comparison
- 31 automated tests

**Files:**
- `translator_agent.py` — CLI translation engine
- `web_app.py` — Flask web interface
- `tests.py` — 31 automated tests
- `templates/` — HTML templates (index.html, results.html)

**Deployment:** Render with BYOK API support

---

### 7. State_Policy_Analysis (v1.4)

**Purpose:** Data-driven analysis of how U.S. states respond to the data center and energy infrastructure boom.

**Key contents:**
- `01_The_Baseline/` — Arkansas legislative architecture (Act 373, Act 548, DATA Act, HB 672)
- `02_CSVs_and_Datasets/` — structured data by state
- `ANALYSIS/` — consolidated analysis for 6 target states (AR, TX, OK, NY, VA, CA)
- `Correlations/` — 42 federal funding withholding events, statistical scripts, DoWhy causal inference
- `Report.md` — full findings report

**Statistical methods:** ANOVA, Kruskal-Wallis, Mann-Whitney U, DoWhy causal inference, temporal lag engine

**Key finding:** No statistically significant relationship between state data center policy posture and federal funding withholding (all p > 0.27). Prior findings transparently corrected when shown to be methodological artifacts.

---

### 8. UVB-76-Structured-Signal-Analysis

**Purpose:** 15-year empirical analysis of Russia's UVB-76 ("The Buzzer") shortwave station transmissions (2010–2025).

**Key findings:** K-means clustering and permutation testing (p < .0005) identified four distinct operational modes and a shift from training-cycle to event-driven signaling correlated with real-world military operations.

---

### 9. leerrooy95.github.io

**Purpose:** Portfolio website.

**Stack:** HTML, CSS, JavaScript

**Contents:** `index.html` (portfolio), `resume.html` (resume), `styles.css`, `main.js`

---

### 10. AI-Manipulation-OSINT-Case-Study

**Purpose:** Quantitative documentation of a 207:1 keyword-frequency disparity across AI platforms with cross-platform verification.

---

### 11. Sovereign-Capital-Audit

**Purpose:** Mapping structural dependencies of the US Defense Industrial Base on Gulf Sovereign Wealth (Mubadala/PIF) and East Asian industry. Tracks capital flows, supply chain vulnerabilities, and national security implications.

---

### 12. Arkansas-Law-Changes-and-AI

**Purpose:** Exploring whether Arkansas eliminated 74 years of citizen initiative protections to clear the path for $17+ billion in AI datacenter development.

---

### 13. Tech_Consolidation_Map

**Purpose:** Tracking data on tech, media, AI, and political consolidation patterns.

---

### 14. Arkansas-DOC-Expenditures-2015-2025

**Purpose:** OCR'd and aggregated Arkansas Department of Corrections expenditure data from scattered PDFs (2015–2025).

---

### 15. Arkansas-Department-of-Corrections-2015-2025-Timeline

**Purpose:** Timeline visualization of Arkansas Department of Corrections data (Python).

---

### 16. AR_Economic_Situation

**Purpose:** Detailed breakdown of Arkansas's economic situation with datasets, data dictionary, sources, and charts.

---

### 17. Layers_of_Control-From_AI_to_Ellison

**Purpose:** OSINT investigation documenting AI engagement manipulation, algorithmic feed control, and Larry Ellison's media consolidation attempts.

---

### 18. Retaliation-and-Solutions_States-Taking-the-Initiative

**Purpose:** Documentation of research retaliation cases and what states/counties can do to protect their citizens.

---

## Commercial Product (In Development)

**Product:** Portable intelligence pipeline architecture packaged as a `.tar.xz` file.

**Store:** [store.regulatedfriction.me](https://store.regulatedfriction.me) — $50 one-time purchase (account verification pending).

**What it includes:** Turnkey setup for an automated OSINT dashboard using the same multi-AI pipeline architecture as Live_Trackers. Minimal configuration — users provide API keys (Brave Search + Anthropic) in GitHub secrets and the pipeline runs automatically. Includes web-grounded fact verification, regulatory capture detection, dual-engine entity extraction (GLiNER2 + optional Llama Scout), interactive entity graph, and nine-tab dashboard. Operating cost under $10/month.

**Note:** Pipeline scripts remain in private repositories. The `.tar.xz` product provides the full pipeline with documentation for independent deployment.

---

## Multi-AI Verification Methodology

A core practice across all projects. No single AI model's output is published without cross-verification.

**Active verification partners:**
- **Anthropic Claude (Opus 4.6 / Sonnet)** — primary research partner, statistical verification, fact-checking pipeline stage
- **Brave Search API** — real-time web search for node tracking, daily intelligence, and fact-check verification. Replaced Perplexity sonar-pro in March 2026.
- **GLiNER2 (local)** — zero-cost entity extraction and relation mapping; runs on CPU inside GitHub Actions with no API call; zero-cost fallback when Llama Scout key is unavailable
- **Meta Llama Scout 17B** — entity extraction and relationship mapping; runs in dual-engine mode alongside GLiNER2 when key is set
- **Google Gemini** — secondary verification partner for cross-checking claims and catching blind spots
- **xAI Grok** — tertiary verification; documented 207:1 bias disparity (see AI-Manipulation-OSINT-Case-Study)
- **GitHub Copilot** — repository management, independent verification of claims before commits, code generation

**How it works:** Each model has documented strengths and blind spots. The pipeline routes tasks to the model best suited for them, then cross-checks outputs across at least two models before publication. Hallucinations caught by this process are documented (see the Gemini "Atlantis Today" incident — a fabricated source caught by Claude's physics validation and documented in the Cuba Crisis Escalation file).

---

## Tech Stack Summary

| Category | Tools |
|----------|-------|
| **Languages** | Python, HTML, CSS, JavaScript |
| **Web frameworks** | Flask |
| **AI/LLM APIs** | Anthropic Claude (Sonnet, Opus 4.6), Brave Search API, Meta Llama Scout 17B, Gradient AI, Google Gemini |
| **Local AI** | GLiNER2 (fastino/gliner2-base-v1) — NER, relation extraction, text classification; runs on CPU, zero API cost |
| **Data** | Pandas, Plotly, SciPy, Textstat, DoWhy, Chart.js |
| **Graph / Visualization** | NetworkX (graph construction + analysis), PyVis (interactive HTML rendering), Chart.js (dashboard charts) |
| **Statistics** | Pearson correlation, Granger causality, permutation testing, bootstrap, ANOVA, Kruskal-Wallis, Mann-Whitney U, chi-square, DoWhy causal inference |
| **Deployment** | GitHub Pages, Render, GitHub Actions, DigitalOcean |
| **Security** | BYOK model, CSRF, rate limiting, DOMPurify, CSP headers, session encryption |

---

## Workflow Patterns

### Automated Intelligence Pipeline (Live_Trackers — private)
```
GitHub Actions (08:00/20:00 UTC)
  → node_tracker.py (Brave Search + Claude)
  → entity_extractor.py (GLiNER2 local + Llama Scout 17B dual-engine)
  → graph_builder.py (NetworkX + PyVis → docs/data/entity_graph.html)
  → convergence_detector.py (local)
  → chart_data_builder.py (local)
  → daily_intelligence.py (Brave Search + Claude)
  → fact_checker.py (Brave Search + Anthropic Claude)
  → rhetoric_reality.py (Anthropic Claude)
  → publish to docs/data/ → regulatedfriction.me
```

### DigitalOcean Scrapers
```
Automated schedule
  → Federal Register scraper → structured data
  → DOJ Press Release scraper → structured data
  → Output feeds into Live_Trackers pipeline
```

### Crypto Monitoring
```
Pipeline monitors USD1/WLF/MGX capital flows
  → Chart.js visualizations on dashboard
  → JSON outputs feed convergence detection
```

### Data Sync (The_Regulated_Friction_Project)
```
GitHub Actions (10:00 UTC daily)
  → sync_from_live_trackers.yml
  → pulls output/ from Live_Trackers into The_Regulated_Friction_Project/output/
```

### BYOK Web Apps (OSINT_ChatBot, Bill_Translator)
```
User → Render (Flask) → User provides API key in browser → Server proxies to Anthropic → Response
Key never stored on disk, only in encrypted session cookie
```

### Multi-AI Verification Loop
```
Research question or claim
  → Primary model generates output (Claude, Brave Search + Claude, or GLiNER2/Llama Scout depending on task)
  → Secondary model cross-checks (different model)
  → Physics/math/logic validation where applicable
  → Copilot verifies via independent web search before repo commits
  → Hallucinations documented when caught
```

### Entity Graph Generation (Stage 2.5)
```
entity_extractor.py outputs extracted_entities.json
  → graph_builder.py reads extracted_entities.json
  → NetworkX builds directed graph (leverage nodes as hubs, entities as leaves)
  → GLiNER2 relation edges added (ownership, investment, conflict, etc.)
  → Cross-node convergence edges added as dashed yellow (HIGH/MEDIUM severity)
  → Performance guard prunes to top 50 nodes by degree (leverage nodes always retained)
  → PyVis renders to docs/data/entity_graph.html (dark theme, color-coded, physics layout)
  
