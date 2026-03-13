# Tools & Workflows Reference

A reference for AI assistants and collaborators. Describes every active repository, tool, pipeline, and deployment so full context doesn't need to be re-gathered each time.

**Author:** Austin Smith ([@Leerrooy95](https://github.com/Leerrooy95))
**Last Updated:** March 13, 2026

---

## Live Deployments

| Service | URL | Hosted On | Source Repo |
|---------|-----|-----------|-------------|
| Live Intelligence Dashboard | [regulatedfriction.me](https://regulatedfriction.me) | GitHub Pages (Live_Trackers) | [Live_Trackers](https://github.com/Leerrooy95/Live_Trackers) |
| Portfolio Website | [leerrooy95.github.io](https://leerrooy95.github.io) | GitHub Pages | [leerrooy95.github.io](https://github.com/Leerrooy95/leerrooy95.github.io) |
| OSINT ChatBot | [personal-chatbot-qej0.onrender.com](https://personal-chatbot-qej0.onrender.com/login) | Render (free tier) | [OSINT_ChatBot](https://github.com/Leerrooy95/OSINT_ChatBot) |
| Bill Translator | [bill-translator.onrender.com](https://bill-translator.onrender.com/) | Render (free tier) | [Bill_Translator](https://github.com/Leerrooy95/Bill_Translator) |

---

## Active Repositories

### 1. The Regulated Friction Project (v10.6)

**Purpose:** Research-only information repository. Documents temporal correlations between geopolitical friction events and institutional capital flows (2015–2026).

**Key contents:**
- 15-section research corpus (00_Quick_Breakdowns through 14_Files)
- `_AI_CONTEXT_INDEX/` — 12 structured markdown files + Node Dossiers used by AI assistants and the OSINT ChatBot
- `Project_Trident/` — independent verification suite (16 statistical tests by Opus 4.6)
- `Run_Correlations_Yourself/` — reproducibility scripts
- `output/` — daily data synced from Live_Trackers

**Workflows:**
- `sync_from_live_trackers.yml` — pulls latest pipeline output from Live_Trackers daily at 10:00 UTC

**Core statistics:** r = +0.6196 (p = 0.0004), 66 verified event pairs, 7-day median lag

**Note:** The Streamlit dashboard has been retired. All live monitoring is now in Live_Trackers. Deprecated files (Streamlit source, Scrapy spider, old workflows) are in `Archive/`.

---

### 2. Live_Trackers (v2.0)

**Purpose:** Unified real-time intelligence pipeline powering the live dashboard at regulatedfriction.me.

**Five-stage pipeline:**

| Stage | Script | AI Model | Function |
|-------|--------|----------|----------|
| 1 | `node_tracker.py` | Perplexity sonar-pro | Queries current status of 7 leverage nodes, classifies events |
| 2 | `entity_extractor.py` | Llama Scout 17B | Extracts entities, relationships, temporal markers from node data |
| 3 | `convergence_detector.py` | Local (no API) | Detects multi-node convergence patterns from historical runs |
| 4 | `daily_intelligence.py` | Perplexity sonar-pro | Tracks 8 signals, scans 59 entities for breaking news, verifies predictions |
| 5 | `fact_checker.py` | Anthropic Claude Sonnet | Fact-checks all output, corrects errors in-place |

**Leverage nodes tracked:** Maxwell, Iran, Gulf SWF, Israel, Oracle/Ellison, Epstein Files, Arkansas Datacenter

**Output:** JSON files in `output/` — node_status, extracted_entities, convergence_report, daily_intelligence, live_verification, fact_check. Timestamped copies in `output/history/`.

**Dashboard:** Static HTML/CSS/JS in `docs/` served via GitHub Pages at regulatedfriction.me. Shows node status cards, intelligence summary, convergence analysis, predictions, entity extraction, history, and fact-check results.

**Workflows:**
- `run_pipeline.yml` — runs the full pipeline twice daily (08:00 / 20:00 UTC), publishes to dashboard
- `deploy.yml` — CI/CD validation on push to main

**API budget:** Node tracker: 50 calls/day. Daily intelligence: 75 calls/day. Llama Scout: 1 call/run. Convergence: no API calls.

**Required secrets:** `PERPLEXITY_API_KEY`, `LLAMA_SCOUT_KEY`, `ANTHROPIC_API_KEY`

---

### 3. OSINT_ChatBot

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

### 4. Bill_Translator

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

### 5. State_Policy_Analysis (v1.4)

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

### 6. UVB-76-Structured-Signal-Analysis

**Purpose:** 15-year empirical analysis of Russia's UVB-76 ("The Buzzer") shortwave station transmissions (2010–2025).

**Key findings:** K-means clustering and permutation testing (p < .0005) identified four distinct operational modes and a shift from training-cycle to event-driven signaling correlated with real-world military operations.

---

### 7. leerrooy95.github.io

**Purpose:** Portfolio website.

**Stack:** HTML, CSS, JavaScript

**Contents:** `index.html` (portfolio), `resume.html` (resume), `styles.css`, `main.js`

---

### 8. AI-Manipulation-OSINT-Case-Study

**Purpose:** Quantitative documentation of a 207:1 keyword-frequency disparity across AI platforms with cross-platform verification.

---

### 9. Sovereign-Capital-Audit

**Purpose:** Mapping structural dependencies of the US Defense Industrial Base on Gulf Sovereign Wealth (Mubadala/PIF) and East Asian industry. Tracks capital flows, supply chain vulnerabilities, and national security implications.

---

### 10. Arkansas-Law-Changes-and-AI

**Purpose:** Exploring whether Arkansas eliminated 74 years of citizen initiative protections to clear the path for $17+ billion in AI datacenter development.

---

### 11. Tech_Consolidation_Map

**Purpose:** Tracking data on tech, media, AI, and political consolidation patterns.

---

### 12. Arkansas-DOC-Expenditures-2015-2025

**Purpose:** OCR'd and aggregated Arkansas Department of Corrections expenditure data from scattered PDFs (2015–2025).

---

### 13. Arkansas-Department-of-Corrections-2015-2025-Timeline

**Purpose:** Timeline visualization of Arkansas Department of Corrections data (Python).

---

### 14. AR_Economic_Situation

**Purpose:** Detailed breakdown of Arkansas's economic situation with datasets, data dictionary, sources, and charts.

---

### 15. Layers_of_Control-From_AI_to_Ellison

**Purpose:** OSINT investigation documenting AI engagement manipulation, algorithmic feed control, and Larry Ellison's media consolidation attempts.

---

### 16. Retaliation-and-Solutions_States-Taking-the-Initiative

**Purpose:** Documentation of research retaliation cases and what states/counties can do to protect their citizens.

---

## Tech Stack Summary

| Category | Tools |
|----------|-------|
| **Languages** | Python, HTML, CSS, JavaScript |
| **Web frameworks** | Flask |
| **AI/LLM APIs** | Anthropic Claude (Sonnet, Opus 4.6), Perplexity sonar-pro, Meta Llama Scout 17B |
| **Data** | Pandas, Plotly, SciPy, Textstat, DoWhy |
| **Statistics** | Pearson correlation, Granger causality, permutation testing, bootstrap, ANOVA, Kruskal-Wallis, Mann-Whitney U, chi-square, DoWhy causal inference |
| **Deployment** | GitHub Pages, Render, GitHub Actions |
| **Security** | BYOK model, CSRF, rate limiting, DOMPurify, CSP headers, session encryption |

---

## Workflow Patterns

### Automated Intelligence Pipeline (Live_Trackers)
```
GitHub Actions (08:00/20:00 UTC)
  → node_tracker.py (Perplexity)
  → entity_extractor.py (Llama Scout 17B)
  → convergence_detector.py (local)
  → daily_intelligence.py (Perplexity)
  → fact_checker.py (Anthropic Claude)
  → publish to docs/data/ → regulatedfriction.me
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

---

## Ignored / Archived Repositories

- **Project_Chrysanthemum** — Japan-China tech integration analysis. Data confidence is low (early learning project); excluded from profile.
- **DOGE_Global_Effects / BRICS-NDB-LocalCurrency-DiD** — Retracted due to Grok-fabricated data. Documented in The_Regulated_Friction_Project `Archive/Retracted_Three_Layer_References.md`.

---

*This file exists so AI assistants and collaborators can quickly understand the full project ecosystem without re-gathering context from each repository.*
