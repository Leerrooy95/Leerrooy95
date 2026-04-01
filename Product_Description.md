# OSINT Intelligence Pipeline — Live Trackers

**One-time purchase · $50 · Instant delivery**

---

## What You Get

A complete, production-ready intelligence pipeline — 34 files, ready to deploy. Push it to GitHub, add your API keys, and it runs itself. Twice a day, every day — no servers, no databases, no babysitting.

The pipeline monitors any set of topics you define, tracks signals across them, extracts entities with dual AI engines, detects multi-node convergence patterns, fact-checks its own output against live web evidence, tracks predictions over time, and publishes everything to a live nine-tab interactive dashboard on your custom domain.

---

## How It Works

The pipeline runs **ten stages** (numbered 1–8, with two half-stages at 6.5 and 7.5) inside GitHub Actions on a cron schedule — fully automated, fully serverless:

1. **Node Tracking** *(Stage 1)* — Queries Brave Search for real-time web results on every topic you configure, then feeds them through Anthropic Claude for classification (`FRICTION`, `COMPLIANCE`, `ESCALATION`, or `DE_ESCALATION`). Entity disambiguation rules prevent the AI from conflating similarly named organisations. A dedicated **Regulatory Capture / Personnel** prompt section flags revolving-door moves, advisory appointments, and executive orders that directly benefit tracked entities — even when they aren't the primary headline.
2. **Entity Extraction** *(Stage 2)* — Dual AI engine: **GLiNER2** runs locally at zero cost for named-entity recognition, while **Llama Scout 17B** (via GitHub Models API) produces structured JSON with entities, relationships, temporal markers, and cross-node connections. Llama Scout is primary when available; GLiNER2 serves as an automatic fallback.
3. **Convergence Detection** *(Stage 3)* — Local analysis that reads your full run history and spots windows where three or more topics show simultaneous activity within a 7-day window. Also identifies friction↔compliance pairs — where one node is in friction while another is in compliance at the same time.
4. **Daily Intelligence** *(Stage 4)* — The most sophisticated stage. Runs a **three-pass intelligence protocol**: (1) an individual signal sweep that queries each signal separately so no single topic can dominate the output, with built-in **contamination detection** that re-queries under-represented signals; (2) a cross-node convergence scan for stories that span multiple topics; and (3) an **under-radar probe** that actively hunts for developments not yet in mainstream coverage. Also manages prediction tracking — active forecasts are verified against new data every run, with a full audit trail of resolved predictions.
5. **Fact Verification** *(Stage 5)* — Three-phase editorial review: inline date/dollar triage catches future dates and ambiguous attributions; Brave Search queries (up to 30 per run) gather live web evidence for each claim; then Anthropic Claude cross-references and **corrects incorrect dates, misattributed actions, and fabricated events in-place** — so the dashboard always shows verified content. Claims are deduplicated before verification (SequenceMatcher >0.70), and corrections propagate back to every upstream file. Standing entity corrections from the config are injected automatically.
6. **Rhetoric vs. Reality** *(Stage 6)* — Three-column gap analysis for each active development: what officials said (rhetoric), what filings and documents show (reality), and what Americans pay for the gap (domestic cost). Includes institutional bypass tracking, ideological driver analysis, and confidence levels (HIGH / MEDIUM / LOW).
7. **Knowledge Base Builder** *(Stage 6.5)* — Generates structured AI context files from entity, convergence, and rhetoric/reality data so a chatbot can answer questions about your intelligence output accurately — updated every run.
8. **Validation** *(Stage 7)* — Cross-stage consistency checks: confirms critical nodes appear in top developments, checks source diversity, flags signal contamination, and verifies convergence events have entity overlap. Non-blocking — logs warnings without stopping the pipeline.
9. **Chart Data** *(Stage 7.5)* — Aggregates your full run history into chart-ready JSON for the dashboard's trend analysis tab.
10. **Interactive Entity Graph** *(Stage 8)* — Builds a directed, interactive HTML network graph of entity relationships using NetworkX and PyVis, served directly from the dashboard. Relationship arrows preserve the directionality captured by entity extraction.

Everything publishes to a static GitHub Pages dashboard — **nine tabs** covering node status, intelligence, convergence, predictions, entities, entity graph, charts, rhetoric vs. reality, and run history.

---

## What's Inside the Package

- **11 Python scripts** — 10 pipeline stage scripts and a knowledge-base context sync utility
- **3 GitHub Actions workflows** — scheduled pipeline (twice daily), validation on every push, and knowledge base sync
- **Static HTML dashboard** — nine-tab interface that reads JSON directly in the browser — no backend required
- **Unified config file** — define your own nodes, signals, tracked entities, disambiguation rules, and standing corrections in one place
- **Shell runner** — local orchestrator with `--dry-run` support for development and testing
- **Full documentation** — setup guide, secrets reference, pipeline architecture walkthrough, and troubleshooting guide
- **Budget trackers** — built-in daily API call limits (50/day for node tracking, 100/day for intelligence) prevent runaway costs

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Web Search | Brave Search API |
| Analysis & Verification | Anthropic Claude Sonnet (stages 1, 4, 5, 6) |
| Entity Extraction | GLiNER2 (local, zero-cost) + Llama Scout 17B (GitHub Models) |
| Graph Visualization | NetworkX + PyVis |
| Automation | GitHub Actions (cron-scheduled, free tier) |
| Dashboard | Static HTML + vanilla JavaScript on GitHub Pages |
| Config | Single JSON file — all nodes, signals, rules, and corrections in one place |

---

## Setup Time: Under 15 Minutes

1. Extract the archive and push to a new GitHub repo
2. Add secrets: `BRAVE_API_KEY` and `ANTHROPIC_API_KEY` (required), plus `LLAMA_SCOUT_KEY` (optional — falls back to GLiNER2-only extraction)
3. Enable GitHub Pages (branch: `main` / `docs`)
4. Click **Run workflow** once — after that it runs itself at 08:00 and 20:00 UTC daily

That's it. No servers. No databases. No Docker. No deployment commands.

---

## Who It's For

- **Researchers** tracking geopolitical, financial, or institutional patterns who need automated, fact-checked reporting
- **OSINT analysts** who want a production intelligence system without building infrastructure from scratch
- **Developers** who want a real-world template for scheduled, multi-stage AI pipelines on GitHub Actions
- **Journalists and investigators** who need a self-updating dashboard that catches under-the-radar stories
- **Anyone** who needs a verified, self-correcting intelligence feed with zero ongoing maintenance

---

## What Makes It Different

- **Self-verifying** — The pipeline fact-checks its own output against live web evidence before publishing. Corrections propagate in-place — the dashboard always shows verified, corrected content.
- **Three-pass intelligence** — Individual signal sweep, cross-node convergence scan, and an under-radar probe that actively finds stories the mainstream press hasn't picked up yet. Signal contamination detection re-queries automatically when one topic starts dominating.
- **Prediction tracking** — Active forecasts are tracked across runs and verified against new data every cycle, with a full audit trail of resolved predictions.
- **Zero infrastructure** — Runs entirely on GitHub Actions free tier. No servers, no Docker, no cloud bills. Built-in budget trackers prevent runaway API costs.
- **Self-healing architecture** — Most stages use `continue-on-error` so a single failure never kills the pipeline. Retry logic with merge-on-conflict handles concurrent pushes. If all API calls fail, the pipeline falls back to the most recent historical data.
- **Fully configurable** — Swap out every tracked topic, signal, entity, disambiguation rule, and standing correction by editing one JSON file. No code changes needed.
- **Dual extraction with automatic fallback** — GLiNER2 runs locally at zero API cost for entity recognition; Llama Scout 17B adds structured relationships and cross-node connections. If one engine is unavailable, the other picks up automatically.
- **Regulatory capture detection** — Dedicated prompt engineering flags revolving-door moves between government and tracked entities, advisory appointments, and executive orders that benefit specific organisations.
- **Interactive entity graph** — A directed, explorable HTML network graph of entity relationships, rendered with NetworkX + PyVis and served from the dashboard.
- **Built-in AI knowledge base** — Every run generates structured context files that a chatbot can use to answer questions about your data accurately — always current.

---

## Live Demo

See the pipeline running in production: **[regulatedfriction.me](https://regulatedfriction.me)**

---

## Support

Questions, issues, or custom build requests: **austin@dvmgservices.com**

Built by Austin Smith — 19D Army veteran, first line of Python in October 2025.

---

*[Terms of Service](https://leroyswebdevelopment.tech/terms.html) · [Privacy Policy](https://leroyswebdevelopment.tech/privacy.html) · [Refund Policy](https://leroyswebdevelopment.tech/refund.html)*
