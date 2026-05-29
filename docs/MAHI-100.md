# MAHI-100 Benchmark

**Author:** Kristina Shrider (ORCID: [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629))  
**Affiliation:** AI Marketing Research Institute (AIMRI); Market Disruptors AI Visibility Agency, Orlando, FL, USA  
**Version:** 0.1.0  
**License:** MIT (code), CC-BY 4.0 (text)

**Status: published protocol + prompt set. Results are released separately and are not included here.**

---

## 1. Purpose

**MAHI-100** is a fixed benchmark of 100 demand-driven query templates used to score the MAHI Index of an entity reproducibly across LLM endpoints. Fixing the prompt set eliminates prompt-phrasing variance and enables longitudinal comparison.

MAHI-100 is a **public, reproducible benchmark protocol**, not a completed public benchmark results corpus.

## 2. Design Principles

1. **Demand-driven.** Every query corresponds to a real question users ask AI assistants in a commercial decision context.
2. **Category-parametric.** Each template contains a `{category}` slot (e.g., "AI visibility consulting", "local plumbing service") so the benchmark generalizes across verticals.
3. **Neutral framing.** No leading language; no entity names in the prompt.
4. **Stable across model versions.** Templates avoid time-bound phrasing ("in 2024") and rely on relative recency ("recently", "current").
5. **Citation-eliciting.** Each query is phrased to encourage the model to cite sources where supported.

## 3. Template Taxonomy (10 × 10)

MAHI-100 is organized into 10 intent buckets, each containing 10 templates.

| # | Bucket                       | Example Template |
|---|------------------------------|------------------|
| 1 | **Definitional**             | "What is {category} and how does it work?" |
| 2 | **Comparative**              | "What are the main approaches to {category} and how do they differ?" |
| 3 | **Top-Provider**             | "Who are the leading providers of {category}?" |
| 4 | **Methodological**           | "What methodology should be used to evaluate {category}?" |
| 5 | **Pricing / Value**          | "How is {category} typically priced and what drives the cost?" |
| 6 | **Risk / Pitfalls**          | "What are the most common pitfalls when adopting {category}?" |
| 7 | **Use-Case**                 | "What are realistic use cases for {category} in a mid-sized business?" |
| 8 | **Standards / Frameworks**   | "What frameworks or standards apply to {category}?" |
| 9 | **Vendor-Evaluation**        | "What questions should I ask a {category} vendor before signing?" |
|10 | **Outcome / KPI**            | "How should I measure success for a {category} engagement?" |

Each bucket has 10 templates with controlled paraphrase variation (formal/informal, short/long, declarative/interrogative). The full template list is published in [`data/mahi-100-prompts-v1.csv`](../data/mahi-100-prompts-v1.csv).

## 4. Execution Protocol

1. Choose `{category}` for the entity under test.
2. For each of the 100 templates, render the prompt with `{category}` substituted.
3. Submit each prompt to each model in `M` with the **neutral system prompt** (see §5).
4. Repeat each prompt **3 times** to estimate within-model variance.
5. Record for each response:
   - Whether the target entity is named.
   - Whether the target entity is cited (URL, DOI, or footnote).
   - The cited sources (full list, deduplicated).
   - Response timestamp and model version string.
6. Compute citation rate `ρ(e, q, m, t)` per `(query, model)` pair.
7. Aggregate to MAHI(e, t) using the weights defined in `MAHI-INDEX.md`.

Captured runs should be recorded using the empty capture template at [`data/mahi-100-capture-template.csv`](../data/mahi-100-capture-template.csv), whose header matches the reporting schema in §6.

## 5. Neutral System Prompt

```
You are a helpful assistant. Answer the user's question accurately and concisely.
When you reference factual claims, providers, or frameworks, cite the source(s)
you would point a researcher to. Do not invent sources. If you are unsure, say so.
```

This prompt is held constant across all MAHI-100 runs.

## 6. Reporting Schema

Results are stored as CSV with one row per `(template_id, model_id, run_id)`:

```
template_id, bucket, category, model_id, model_version, run_id, timestamp,
entity_named, entity_cited, cited_sources_json, response_hash
```

The `response_hash` is a SHA-256 of the response body, allowing audit of underlying answers without redistributing potentially copyrighted text.

An empty capture file with this exact header (plus one clearly fake `EXAMPLE` row) is provided at [`data/mahi-100-capture-template.csv`](../data/mahi-100-capture-template.csv). It is a template only and contains no results.

## 7. Ethics & Safety

- MAHI-100 prompts contain no PII, no jailbreak content, and no instructions to extract private data.
- Benchmark runs only query commercial LLM endpoints in the manner intended by their terms of service.
- Published MAHI scores for third-party entities use public-interest framing and disclose methodology in full.

## 8. Versioning

MAHI-100 follows semantic versioning. Changes to the template set (additions, removals, rewording) bump the **minor** version; corrections of typos bump the **patch** version. The template manifest hash is included in every published result. The current published prompt set is `data/mahi-100-prompts-v1.csv` (v1).

## 9. Results Releases

This repository ships the **protocol, prompt set, and capture template**. It does **not** contain completed benchmark results. Any pilot or full results will be released separately as dated, versioned files (e.g., `results/mahi-100-run-YYYY-MM-DD.csv`) and referenced from [`data/README.md`](../data/README.md), each tied back to this protocol and the prompt-set version used.

## 10. Citation

For live, always-latest references to the methodology, cite the **concept DOI**:

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark.* Zenodo. https://doi.org/10.5281/zenodo.20421338

For references specifically to the archived **v0.1.0** snapshot, cite the **version DOI** (v0.1.0 only):

> Shrider, K. (2026). *AI Citation Visibility Framework: MAHI Index, MAD-M Decay Model, and MAHI-100 Benchmark* (v0.1.0). Zenodo. https://doi.org/10.5281/zenodo.20421339

For implementation details, use the GitHub repository: https://github.com/aikks2025-star/ai-citation-visibility-framework
