# AI Citation Visibility Framework

[![DOI (concept, latest)](https://zenodo.org/badge/DOI/10.5281/zenodo.20421338.svg)](https://doi.org/10.5281/zenodo.20421338)
[![DOI (v0.2.2)](https://zenodo.org/badge/DOI/10.5281/zenodo.20450041.svg)](https://doi.org/10.5281/zenodo.20450041)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ORCID](https://img.shields.io/badge/ORCID-0009--0002--2655--4629-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0009-0002-2655-4629)

How AI systems decide which businesses to cite. A reproducible, model-agnostic measurement framework for AI visibility across **ChatGPT, Claude, Perplexity, Google AI Overviews, and Microsoft Copilot**.

This repository is the canonical source-of-truth for three primitives:

- **MAHI Index** — Marketing Agent Health Index ([`docs/MAHI-INDEX.md`](docs/MAHI-INDEX.md))
- **MAD-M** — Marketing Agent Decay Model, a governance-first heuristic ([`docs/MAD-M.md`](docs/MAD-M.md))
- **MAHI-100** — a public, reproducible 100-prompt benchmark protocol ([`docs/MAHI-100.md`](docs/MAHI-100.md))

Author: **Kristina Shrider** — ORCID [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629)  
Affiliation: AI Marketing Research Initiative (AIMRI); Market Disruptors AI Visibility Agency — Orlando, FL, USA.

Public documentation and applied methodology are maintained by Market Disruptors AI Visibility Agency:

- MAHI-100 protocol: https://marketdisruptorsagency.com/mahi-100
- MAD-M framework: https://marketdisruptorsagency.com/mad-m-framework
- MAHI Index: https://marketdisruptorsagency.com/mahi-index
- AI discovery methodology: https://marketdisruptorsagency.com/ai-discovery
- Founder and research profile: https://marketdisruptorsagency.com/about/kristina

---

## What this framework answers

> *"How do generative AI assistants decide which businesses to cite, and how do I measure (and improve) my entity's standing in that citation graph?"*

The framework defines:

1. **A score (MAHI)** — a `[0, 100]` composite from five publicly observable sub-indices: Entity Resolution, Citation Surface, Semantic Coverage, Freshness, and Trust Graph.
2. **A decay model (MAD-M)** — a governance-first heuristic describing how AI-mediated marketing systems can lose visibility, attribution, and authority over time without fresh sourcing, provenance, differentiation, and review. MAD-M is a planning lens, not a predictive model.
3. **A benchmark (MAHI-100)** — a fixed `10 × 10` taxonomy of demand-driven query templates, executed against a fixed model set with a neutral system prompt to produce reproducible, longitudinal measurements.

---

## MAD-M 12-week drift scenario

MAD-M includes a **12-week drift scenario** used as a heuristic planning lens for content governance and refresh cycles. It is not a guaranteed prediction, ranking forecast, or fixed traffic timeline.

| Phase | Timing | Risk State |
|-------|--------|------------|
| Freshness Advantage | Weeks 1-2 | Optimal |
| Pattern Recognition | Weeks 3-4 | Caution |
| Confidence Erosion | Weeks 5-6 | Caution |
| Authority Decay | Weeks 7-8 | High Risk |
| Systemic Deprioritization | Weeks 9+ | Critical |

Use MAHI to diagnose current AI visibility health. Use MAD-M and the 12-week drift scenario to plan review, source-refresh, provenance, and content-governance cycles before unmanaged assets lose retrievability or citation share.

---

## MAHI-100 protocol & data

MAHI-100 is a **public, reproducible 100-prompt benchmark protocol**. This repo ships the protocol, the prompt set, and an empty capture template:

- Protocol / methodology: [`docs/MAHI-100.md`](docs/MAHI-100.md)
- Prompt set (v1, 100 templates, `{category}` slot): [`data/mahi-100-prompts-v1.csv`](data/mahi-100-prompts-v1.csv)
- Empty capture template (headers + one `EXAMPLE` row): [`data/mahi-100-capture-template.csv`](data/mahi-100-capture-template.csv)
- Data directory notes: [`data/README.md`](data/README.md)

### Reproduction quickstart

1. **Choose a category.** Pick the `{category}` value for the entity under test (e.g., "AI visibility consulting").
2. **Apply it to the 100 prompt templates.** Substitute `{category}` into every row of `data/mahi-100-prompts-v1.csv`.
3. **Run the prompts across selected AI systems.** Use the neutral system prompt in `docs/MAHI-100.md` §5, across the model set you choose.
4. **Record outputs using the capture template.** Log each response in a copy of `data/mahi-100-capture-template.csv` following the schema in `docs/MAHI-100.md` §6.

> **This repo ships the protocol, prompt set, and capture template. It does not contain completed benchmark results.** Any pilot or full results will be released separately as dated, versioned files and referenced from [`data/README.md`](data/README.md).

## Citation definition layer

The repository also ships a machine-readable definition layer for the non-branded AI visibility questions Market Disruptors AI Visibility Agency is targeting:

- Citation map: [`docs/CITATION-MAP.md`](docs/CITATION-MAP.md)
- AI citation decay: [`docs/definitions/ai-citation-decay.md`](docs/definitions/ai-citation-decay.md)
- Shortlist economy: [`docs/definitions/shortlist-economy.md`](docs/definitions/shortlist-economy.md)
- AI agent brand selection: [`docs/definitions/ai-agent-brand-selection.md`](docs/definitions/ai-agent-brand-selection.md)
- Getting cited by ChatGPT: [`docs/definitions/get-cited-by-chatgpt.md`](docs/definitions/get-cited-by-chatgpt.md)
- Getting cited by Perplexity: [`docs/definitions/get-cited-by-perplexity.md`](docs/definitions/get-cited-by-perplexity.md)
- AI provenance in marketing: [`docs/definitions/ai-provenance-marketing.md`](docs/definitions/ai-provenance-marketing.md)
- Ads in AI search: [`docs/definitions/ads-in-ai-search.md`](docs/definitions/ads-in-ai-search.md)
- Agentic commerce for marketing visibility: [`docs/definitions/agentic-commerce-marketing.md`](docs/definitions/agentic-commerce-marketing.md)

---

## How to cite

**Cite the latest version (concept DOI):**

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark.* Zenodo. https://doi.org/10.5281/zenodo.20421338

**Cite v0.2.2 specifically (version DOI):**

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark* (v0.2.2). Zenodo. https://doi.org/10.5281/zenodo.20450041

Machine-readable citation metadata is available in [`CITATION.cff`](CITATION.cff) and [`codemeta.json`](codemeta.json).

## License

- **Code:** [MIT](LICENSE)
- **Documentation in `/docs`:** CC-BY 4.0 (see in-file headers)

## Ethics

All inputs to the framework are publicly observable. No PII, no scraped credentialed data, no jailbreak content. Forensic case studies built on this framework follow public-interest framing and undergo legal review before publication.

## Repository layout

```
.
├── README.md            — this file
├── LICENSE              — MIT
├── CITATION.cff         — Citation File Format metadata
├── codemeta.json        — CodeMeta / schema.org metadata
├── .zenodo.json         — Zenodo deposit metadata
├── data/
│   ├── README.md                        — data directory notes (no results)
│   ├── mahi-100-prompts-v1.csv          — 100 MAHI-100 prompt templates
│   └── mahi-100-capture-template.csv    — empty capture template
└── docs/
    ├── CITATION-MAP.md  — website/GitHub/DOI citation target map
    ├── MAHI-INDEX.md    — full MAHI Index definition
    ├── MAD-M.md         — Marketing Agent Decay Model (governance heuristic)
    ├── MAHI-100.md      — MAHI-100 benchmark protocol specification
    └── definitions/     — non-branded AI visibility definition layer
```
