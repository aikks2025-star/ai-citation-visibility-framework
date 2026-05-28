# AI Citation Visibility Framework

[![DOI (concept, latest)](https://zenodo.org/badge/DOI/10.5281/zenodo.20421338.svg)](https://doi.org/10.5281/zenodo.20421338)
[![DOI (v0.1.0)](https://zenodo.org/badge/DOI/10.5281/zenodo.20421339.svg)](https://doi.org/10.5281/zenodo.20421339)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ORCID](https://img.shields.io/badge/ORCID-0009--0002--2655--4629-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0009-0002-2655-4629)

How AI systems decide which businesses to cite. A reproducible, model-agnostic measurement framework for AI visibility across **ChatGPT, Claude, Perplexity, Google AI Overviews, and Microsoft Copilot**.

This repository is the canonical source-of-truth for three primitives:

- **MAHI Index** — Marketing Agent Health Index ([`docs/MAHI-INDEX.md`](docs/MAHI-INDEX.md))
- **MAD-M** — Marketing Agent Decay Model ([`docs/MAD-M.md`](docs/MAD-M.md))
- **MAHI-100** — a 100-query benchmark for AI citation visibility ([`docs/MAHI-100.md`](docs/MAHI-100.md))

Author: **Kristina Shrider** — ORCID [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629)  
Affiliation: AI Marketing Research Institute (AIMRI); Market Disruptors Agency — Orlando, FL, USA.

---

## What this framework answers

> *"How do generative AI assistants decide which businesses to cite, and how do I measure (and improve) my entity's standing in that citation graph?"*

The framework defines:

1. **A score (MAHI)** — a `[0, 100]` composite from five publicly observable sub-indices: Entity Resolution, Citation Surface, Semantic Coverage, Freshness, and Trust Graph.
2. **A decay model (MAD-M)** — an exponential model of how the MAHI score erodes over time without new authoritative signals, decomposed into four drivers (index churn, model churn, competition, canonical drift).
3. **A benchmark (MAHI-100)** — a fixed `10 × 10` taxonomy of demand-driven query templates, executed against a fixed model set with a neutral system prompt to produce reproducible, longitudinal measurements.

## How to cite

**Cite the latest version (concept DOI):**

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark.* Zenodo. https://doi.org/10.5281/zenodo.20421338

**Cite v0.1.0 specifically (version DOI):**

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark* (v0.1.0). Zenodo. https://doi.org/10.5281/zenodo.20421339

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
└── docs/
    ├── MAHI-INDEX.md    — full MAHI Index definition
    ├── MAD-M.md         — Marketing Agent Decay Model
    └── MAHI-100.md      — MAHI-100 benchmark specification
```
