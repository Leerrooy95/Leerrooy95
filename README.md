![Python](https://img.shields.io/badge/Python-3670A0?style=flat&logo=python&logoColor=ffdd54)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat&logo=flask&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic_API-191919?style=flat&logo=anthropic&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=github-actions&logoColor=white)
![HTML/CSS/JS](https://img.shields.io/badge/HTML%2FCSS%2FJS-E34F26?style=flat&logo=html5&logoColor=white)
![Render](https://img.shields.io/badge/Render-46E3B7?style=flat&logo=render&logoColor=white)
![Statistics](https://img.shields.io/badge/Statistics-Correlation%20|%20Permutation%20Testing%20|%20Granger%20Causality-blue)

## Threat Intelligence Analyst | OSINT & Quantitative Methods

**19D Army Veteran** building automated intelligence pipelines, live analytical dashboards, OSINT chatbots, and civic technology tools. I wrote my first line of Python in October 2025.

**[🌐 Portfolio →](https://leerrooy95.github.io)** · **[📊 Live Dashboard →](https://regulatedfriction.me)** · **[🤖 OSINT ChatBot →](https://personal-chatbot-qej0.onrender.com/login)** · **[📜 Bill Translator →](https://bill-translator.onrender.com/)**

---

### 📌 Featured Projects

**[The Regulated Friction Project](https://github.com/Leerrooy95/The_Regulated_Friction_Project)** *(v10.6)* — Research repository documenting temporal correlations between geopolitical friction events and institutional capital flows. Processed 8 years of data across 66 verified event pairs. Independently stress-tested by 16 statistical robustness scripts (Opus 4.6). Includes a structured AI context index (12 files + node dossiers), reproducible correlation scripts, and a 15-section research corpus. Live monitoring has moved to the [Live_Trackers](https://github.com/Leerrooy95/Live_Trackers) pipeline.

| Finding | Value |
|---------|-------|
| Core correlation | r = +0.6196 (p = 0.0004) |
| Convergence correlation | r = +0.6685 (p < 0.0001, n = 229 weeks) |
| Robustness | Permutation (p < 0.001), Granger causality (F = 32.49, p < 0.0001), bootstrap (p = 0.008) |
| Independent verification | 16 statistical tests by Opus 4.6 — all passed |
| Predictions | 25 falsifiable — 4 publicly failed, 11 confirmed, rest tracked |

**[Live Trackers](https://github.com/Leerrooy95/Live_Trackers)** *(v2.0)* — Unified five-stage intelligence pipeline powering the live dashboard at [regulatedfriction.me](https://regulatedfriction.me). Runs twice daily via GitHub Actions: Perplexity sonar-pro queries node status → Llama Scout 17B extracts entities → local convergence detection → daily intelligence with signal tracking and prediction verification → Anthropic Claude fact-checks all output. Monitors 7 leverage nodes, 8 active signals, and 59 tracked entities with entity disambiguation and automated API budgeting.

**[OSINT ChatBot](https://github.com/Leerrooy95/OSINT_ChatBot)** — BYOK (Bring Your Own Key) Flask chatbot deployed on Render. Users provide their own Anthropic API key — the server never stores it. The knowledge base is loaded from the project's `_AI_CONTEXT_INDEX/` at startup and injected into every system prompt. Features rate limiting, CSRF protection, DOMPurify sanitization, and full security headers.

**[Bill Translator](https://github.com/Leerrooy95/Bill_Translator)** — Production Flask web application that rewrites dense legal text to meet 8th-grade readability standards while preserving exact legal intent. Built to address Arkansas Act 602. Features custom meaning drift detection, three translation modes (full simplification, preserve legal terms, jargon-only), automated Flesch-Kincaid scoring, and 31 automated tests. Deployed on Render with BYOK API support.

**[State Policy Analysis](https://github.com/Leerrooy95/State_Policy_Analysis)** *(v1.4)* — Data-driven analysis of how U.S. states are responding to the data center and energy infrastructure boom. Tracks 42 federal funding withholding events across 27 states, classified by data center policy posture. Includes six statistical tests (ANOVA, Kruskal-Wallis, DoWhy causal inference), transparent corrections of prior findings, and the five-stage federal action timeline.

**[UVB-76 Signal Analysis](https://github.com/Leerrooy95/UVB-76-Structured-Signal-Analysis)** — 15-year empirical analysis of Russia's UVB-76 shortwave station. K-means clustering and permutation testing (p < .0005) identified four distinct operational modes and a shift from training-cycle to event-driven signaling correlated with real-world military operations.

---

### 📈 How I Got Here

Started with **[UVB-76](https://github.com/Leerrooy95/UVB-76-Structured-Signal-Analysis)** — gathering data by hand, learning pattern recognition from raw signals.

Middle repos taught me the hard way about AI hallucinations. Those repos are corrected and kept public as lessons in data verification.

Picked up from there by downloading scattered **[Arkansas Department of Corrections](https://github.com/Leerrooy95/Arkansas-DOC-Expenditures-2015-2025)** PDFs, OCR'ing them into clean datasets, and analyzing spending patterns that hadn't been aggregated before.

**[The Regulated Friction Project](https://github.com/Leerrooy95/The_Regulated_Friction_Project)** is where methodology caught up with ambition — automated scraping, statistical validation, reproducible findings, and a live intelligence dashboard. Now at v10.6 with 16 independent robustness tests, a structured AI context index, and a research corpus spanning 15 sections.

**[Live Trackers](https://github.com/Leerrooy95/Live_Trackers)** consolidated everything operational into a five-stage pipeline — node tracking, entity extraction, convergence detection, daily intelligence, and fact-checking — all running on GitHub Actions and publishing to a live static dashboard at [regulatedfriction.me](https://regulatedfriction.me).

**[State Policy Analysis](https://github.com/Leerrooy95/State_Policy_Analysis)** applied the same rigor at the state level — tracking data center legislation across 27 states, running causal inference (DoWhy), and transparently correcting three prior findings that turned out to be methodological artifacts.

**[Bill Translator](https://github.com/Leerrooy95/Bill_Translator)** proved I could build production tools, not just research — a deployed Flask application with real users solving a real legislative transparency problem.

**[OSINT ChatBot](https://github.com/Leerrooy95/OSINT_ChatBot)** extended the research into an interactive BYOK chatbot — giving anyone access to query the full knowledge base through Claude, with proper security, rate limiting, and session management.

---

### 🔧 What I Build

- **Automated OSINT pipelines** — multi-agent LLM extraction (Perplexity → Llama Scout → Claude), entity disambiguation, convergence detection, fact-checking
- **Temporal correlation frameworks** — lag analysis, permutation testing, Granger causality, convergence modeling, DoWhy causal inference
- **Live dashboards** — Static HTML/CSS/JS dashboard at regulatedfriction.me, fed by GitHub Actions twice daily
- **AI-powered chatbots** — BYOK Flask apps with knowledge base injection, session security, and rate limiting
- **Civic technology** — Flask web apps with NLP, meaning drift detection, and readability scoring
- **State-level policy analysis** — federal funding tracking, posture classification, temporal lag engines, transparent corrections
- **Reproducible research** — every finding ships with the scripts to verify it; failed predictions documented publicly

---

### 🤝 Open To

- Threat intelligence and OSINT analyst roles
- Investigative data support and newsroom partnerships
- Temporal pattern analysis and capital flow tracking
- Open-source collaboration on accountability tools

**Contact:** Discord and email in profile description

---

**Last Updated:** *March 13, 2026*
