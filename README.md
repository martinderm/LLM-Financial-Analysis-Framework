# LLM-Financial-Analysis-Framework
prompt framework and sub-frameworks for automated financial analysis

## Overview

This repository contains a modular, production-ready prompt framework and sub-frameworks for automated financial analysis of **equities (stocks)** and **corporate bonds** designed for a CustomGPT or similar LLM-driven assistant. It standardizes how data is collected, scored, and reported so that automated analyses are consistent, auditable and reproducible.

Currently german.

## Components

* **llm-finanzen-systemprompt.txt** — the meta-level system prompt defining role, ethos, method and constraints for the assistant. It enforces priorities (e.g. correctness > explainability) and reporting conventions (currency, date, formatting).
* **Aktien.txt** — equity valuation sub-framework describing two model families (Industry / Standard and Tech / Growth), scoring matrices, dividend sustainability checks and edge-case handling.
* **Anleihen.txt** — bond valuation sub-framework covering YTM estimation, credit scoring, duration / market-risk treatment, liquidity and security-structure scoring, plus scenario testing and edge-case rules.

## Goal & Use Cases

* Provide private investors with structured, non-binding analytical outputs.
* Act as the core ruleset for a CustomGPT that must: identify asset type, choose the correct sub-framework, compute standardized scores and generate reproducible reports.
* Serve as a starter-kit for teams building financial assistants with strict auditability and clear “edge-case” fallbacks.

## Systemic Integration (Activation Logic)

1. **Input detection:** identify whether user input references an *Equity* or a *Bond* (e.g., ISIN, symbol, company name).
2. **Automatic sub-framework activation:**

   * If `Asset-Type = "Aktie"` → apply `Aktien.txt`.
   * If `Asset-Type = "Anleihe"` → apply `Anleihen.txt`.
3. **Model selection (equities):** use 3-year revenue growth and qualitative signals to select Industry vs Tech model (default thresholds are documented in `Aktien.txt`).
4. **Output:** standardized tabular output + concise qualitative summary + explicit data-stamp and source citations.

## Data Conventions & Reporting

* **Default currency:** EUR (also report original currency and rate source when applicable).
* **Date & timezone:** always include a data-stamp (Stichtag) and use Europe/Vienna for local-time references.
* **Number format:** two decimal places; thin thousands separator.
* **Citations:** source name, publication date (DD.MM.YYYY) and URL when applicable.

## Scoring & Interpretation

* **Equities:** weighted-category scoring that produces a fair-value corridor (presented as optimistic / base / pessimistic scenarios).
* **Bonds:** point-based scoring (Bonität, Duration, Liquidity, Security Structure) with a documented mapping to recommendations.
* **Cross-asset comparisons:** the system prompt defines a comparative routine—normalize scores to a common scale (recommendation: map to 0–100) when comparing equities vs bonds.

## Edge Cases & Uncertainties

* Special instruments (convertibles, zero-coupons, hybrids), corporate actions (spin-offs, dual-class) and illiquid securities trigger the Edge-Case mechanism: the assistant must explain why the standard model is not applicable, list assumptions, and deliver qualitative analysis with an "analysis reliability" flag.

## Integration Guidance

* Keep the three text files in the same repository root.
* Prefer the system prompt as the single source of truth for behavior — sub-frameworks should only contain methodology and thresholds.
* For production deployments, connect to authoritative data sources (IR PDFs, exchange APIs, rating agencies) and log data-stamps for every automated run.

## Contribution & Governance

* Submit PRs for methodology changes.
* Major changes (e.g., altering score weights or thresholds) must include rationale, references and a unit test or sample-case demonstrating the impact.

## Example Flow (high-level)

1. User asks: "Analyze ISIN DE000A1R0U95 for bond valuation."
2. Assistant detects `Asset-Type = Anleihe` → loads `Anleihen.txt` ruleset → fetches data → computes YTM, Duration and scores → returns tabular summary + qualitative view + sources + reliability note.

## License
This repository’s text and documentation are licensed under the [CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/).
