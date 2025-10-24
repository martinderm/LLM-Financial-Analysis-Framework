# LLM-Finanzanalyse-Framework
Prompt-Framework und Sub-Frameworks für automatisierte Finanzanalyse

## Überblick

Dieses Repository enthält ein modulares, produktionsreifes Prompt-Framework mit Sub-Frameworks für die automatisierte Finanzanalyse von **Aktien** und **Unternehmensanleihen**, entwickelt für ein CustomGPT oder ein vergleichbares LLM-basiertes Assistenzsystem. Es standardisiert die Datenerhebung, Bewertung und Berichterstattung, sodass Analysen konsistent, nachvollziehbar und prüfbar sind.

## Komponenten

* **llm-finanzen-systemprompt.txt** – das Meta-Systemprompt, das Rolle, Ethos, Methodik und Grenzen des Assistenten definiert. Es legt Prioritäten fest (z. B. Richtigkeit > Verständlichkeit) und standardisiert Berichtsformate (Währung, Datum, Zahlenformat).
* **Aktien.txt** – Bewertungs-Subframework für Aktien mit zwei Modelltypen (Industrie/Standard und Tech/Wachstum), Bewertungsmatrix, Dividendenanalyse und Edge-Case-Regeln.
* **Anleihen.txt** – Bewertungs-Subframework für Unternehmensanleihen mit YTM-Berechnung, Bonitätsscore, Duration- und Zinsrisikoanalyse, Liquiditäts- und Sicherheitenbewertung sowie Szenario- und Sonderfalllogik.

## Praktische Anwendung

Je nach LLM-Plattform erstelle ein neues Projekt, CustomGPT, TailoredAI, Skill oder Agent. Verwende die Datei `llm-finanzen-systemprompt.txt` als **System- oder Instruktionsprompt**. Lade die Dateien `Aktien.txt` und `Anleihen.txt` als **Wissensquellen**, um dem Assistenten die Bewertungsmodelle und Bewertungslogiken zur Verfügung zu stellen.

* **Setup:** Füge den Inhalt von `llm-finanzen-systemprompt.txt` in das Systemprompt-Feld der jeweiligen Plattform ein.
* **Wissensintegration:** Lade `Aktien.txt` und `Anleihen.txt` in die Wissensbasis oder den Dateispeicher, damit das Modell auf deren Methodik zugreifen kann.
* **Ausführung:** Erkennt der Assistent eine Aktie oder Anleihe, wird automatisch das entsprechende Subframework aktiviert, die Bewertungslogik angewendet und das Ergebnis standardisiert ausgegeben.

## Ziel & Anwendungsfälle

* Bereitstellung strukturierter, nicht-bindender Analysen für Privatanleger.
* Nutzung als Kernregelwerk für ein CustomGPT, das Asset-Typen erkennt, passende Bewertungsframeworks auswählt, standardisierte Scores berechnet und reproduzierbare Berichte erstellt.
* Grundlage für Entwicklerteams, die prüfbare Finanzassistenten mit klaren Edge-Case-Regeln bauen wollen.

## Systemische Einbindung (Aktivierungslogik)

1. **Eingangserkennung:** Erkennen, ob der Input eine *Aktie* oder *Anleihe* betrifft (z. B. ISIN, Tickersymbol, Unternehmensname).
2. **Automatische Subframework-Aktivierung:**

   * Wenn `Asset-Type = "Aktie"` → `Aktien.txt` anwenden.
   * Wenn `Asset-Type = "Anleihe"` → `Anleihen.txt` anwenden.
3. **Modellauswahl (Aktien):** Auswahl zwischen Industrie- und Tech-Modell anhand des 3-Jahres-Umsatzwachstums und qualitativer Kriterien (Schwellenwerte siehe `Aktien.txt`).
4. **Ausgabe:** Standardisierte Tabelle + kurze qualitative Zusammenfassung + Quellen- und Datumsangabe.

## Datenkonventionen & Reporting

* **Standardwährung:** EUR (ggf. Originalwährung und Wechselkursquelle angeben).
* **Datum & Zeitzone:** Immer Stichtag angeben; Zeitzone Europe/Vienna.
* **Zahlenformat:** Zwei Dezimalstellen; schmales Tausendertrennzeichen.
* **Quellenangabe:** Quellenname, Veröffentlichungsdatum (TT.MM.JJJJ) und URL.

## Bewertung & Interpretation

* **Aktien:** Gewichtete Kategorienbewertung zur Ermittlung eines Fair-Value-Korridors (optimistisch / Basis / pessimistisch).
* **Anleihen:** Punktbewertungssystem (Bonität, Duration, Liquidität, Sicherheitenstruktur) mit Zuordnung zu Handlungsempfehlungen.

## Sonderfälle & Unsicherheiten

* Besondere Instrumente (z. B. Wandelanleihen, Nullkuponanleihen, Hybride), Unternehmensmaßnahmen (Spin-offs, Dual-Class-Shares) oder illiquide Titel aktivieren den **Edge-Case-Mechanismus**: Der Assistent erklärt, warum das Standardmodell nicht anwendbar ist, dokumentiert Annahmen und liefert eine qualitative Bewertung mit einem Hinweis zur Zuverlässigkeit.

## Beispielablauf (High-Level)

1. Nutzer fragt: „Analysiere ISIN DE000A1R0U95 für eine Anleihebewertung.“
2. Assistent erkennt `Asset-Type = Anleihe` → lädt `Anleihen.txt` → zieht Daten → berechnet YTM, Duration und Scores → liefert Tabelle + qualitative Einschätzung + Quellenhinweis.

## License
This repository’s text and documentation are licensed under the [CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/).

# LLM-Financial-Analysis-Framework (English)
prompt framework and sub-frameworks for automated financial analysis

## Overview

This repository contains a modular, production-ready prompt framework and sub-frameworks for automated financial analysis of **equities (stocks)** and **corporate bonds** designed for a CustomGPT or similar LLM-driven assistant. It standardizes how data is collected, scored, and reported so that automated analyses are consistent, auditable and reproducible.

Currently german.

## Components

* **llm-finanzen-systemprompt.txt** — the meta-level system prompt defining role, ethos, method and constraints for the assistant. It enforces priorities (e.g. correctness > explainability) and reporting conventions (currency, date, formatting).
* **Aktien.txt** — equity valuation sub-framework describing two model families (Industry / Standard and Tech / Growth), scoring matrices, dividend sustainability checks and edge-case handling.
* **Anleihen.txt** — bond valuation sub-framework covering YTM estimation, credit scoring, duration / market-risk treatment, liquidity and security-structure scoring, plus scenario testing and edge-case rules.

## Practical Usage

Depending on your LLM platform, create a new Project, CustomGPT, TailoredAI, Skill, or Agent. Use the `llm-finanzen-systemprompt.txt` file as the **system or instruction prompt**.  Load the `Aktien.txt` and `Anleihen.txt` files as **knowledge sources** to provide the assistant with the underlying valuation frameworks and scoring models.

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

## Edge Cases & Uncertainties

* Special instruments (convertibles, zero-coupons, hybrids), corporate actions (spin-offs, dual-class) and illiquid securities trigger the Edge-Case mechanism: the assistant must explain why the standard model is not applicable, list assumptions, and deliver qualitative analysis with an "analysis reliability" flag.

## Example Flow (high-level)

1. User asks: "Analyze ISIN DE000A1R0U95 for bond valuation."
2. Assistant detects `Asset-Type = Anleihe` → loads `Anleihen.txt` ruleset → fetches data → computes YTM, Duration and scores → returns tabular summary + qualitative view + sources + reliability note.

## License
This repository’s text and documentation are licensed under the [CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/).
