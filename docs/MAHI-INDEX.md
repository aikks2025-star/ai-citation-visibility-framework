# MAHI Index (Marketing Agent Health Index)

**Author:** Kristina Shrider (ORCID: [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629))  
**Affiliation:** AI Marketing Research Initiative (AIMRI); Market Disruptors AI Visibility Agency, Orlando, FL, USA
**Version:** 0.1.0  
**License:** MIT (code), CC-BY 4.0 (text)

---

## 1. Definition

The **Marketing Agent Health Index (MAHI)** is a composite scalar in the range `[0, 100]` that estimates the probability that a generative AI assistant (ChatGPT, Claude, Perplexity, Google AI Overviews, Microsoft Copilot) will cite a given business entity when answering a category-relevant, demand-driven query.

MAHI is designed to be:

- **Reproducible** — computed from publicly observable signals only.
- **Model-agnostic** — same inputs scored against multiple LLM endpoints.
- **Time-indexed** — every score carries a measurement timestamp (`t`) to enable decay analysis via MAD-M.

## 2. Component Sub-Indices

MAHI is the weighted sum of five sub-indices, each normalized to `[0, 100]`:

| Symbol | Sub-Index                          | Default Weight |
|--------|------------------------------------|---------------:|
| `E`    | Entity Resolution Score            | 0.25 |
| `C`    | Citation Surface Score             | 0.25 |
| `S`    | Semantic Coverage Score            | 0.20 |
| `F`    | Freshness Score                    | 0.15 |
| `T`    | Trust Graph Score                  | 0.15 |

```
MAHI(e, q, t) = 0.25 · E + 0.25 · C + 0.20 · S + 0.15 · F + 0.15 · T
```

Where `e` is the entity under measurement, `q` is the query (or query cluster), and `t` is the measurement timestamp.

### 2.1 Entity Resolution (E)

Measures whether the entity is unambiguously resolvable in the public knowledge graph layer that LLMs and retrieval systems consult.

Signals (each contributes equally unless re-weighted):

- Wikidata QID present and populated (instance-of, founder, located-in, official website).
- ORCID, ROR, or other authoritative identifier present.
- Schema.org `Organization` / `Person` JSON-LD on the canonical site.
- Consistent NAP (Name, Address, Phone) across at least 5 authoritative directories.
- Canonical URL declared and stable across crawls.

### 2.2 Citation Surface (C)

Measures the density and quality of inbound citations from sources LLMs are known to weight heavily during pretraining and retrieval.

Signals:

- Indexed presence on Zenodo, OpenAlex, Crossref, SSRN, ResearchGate, Academia.edu.
- Backlinks from `.edu`, `.gov`, and recognized industry publications.
- GitHub repository with non-trivial activity and a DOI-minted release.
- Mentions in Common Crawl snapshots within the last 12 months.

### 2.3 Semantic Coverage (S)

Measures how completely the entity's public content covers the *demand-driven question space* of its category.

Signals:

- Number of distinct FAQ schema answers published on canonical site.
- Coverage of the top-N (default N=100) People-Also-Ask questions for the category.
- Presence of definitional, methodological, and comparative content (not only promotional).
- Average answer length ≥ 40 words and ≤ 120 words (LLM-friendly chunk size).

### 2.4 Freshness (F)

Measures the recency of authoritative content updates.

Signals:

- Last-modified timestamp on canonical pages within last 90 days.
- New publication (paper, dataset, release) within last 180 days.
- Active commit history on associated repositories.

### 2.5 Trust Graph (T)

Measures the strength of the entity's position in the cross-platform trust graph.

Signals:

- ORCID-verified authorship of cited works.
- Co-citation with high-authority entities in the same category.
- Verified profiles on at least 3 of: LinkedIn, Crossref, ORCID, Wikidata, GitHub.
- Absence of contradictory entity records (duplicates, conflicting affiliations).

## 3. Measurement Protocol

1. Fix the query set `Q` (default: MAHI-100 benchmark, see `MAHI-100.md`).
2. Fix the model set `M` (default: ChatGPT-4o, Claude 3.5 Sonnet, Perplexity Sonar, Google AI Overviews, Microsoft Copilot).
3. For each `(q, m)` pair, issue the query three times with neutral system prompt and record whether entity `e` appears in the cited sources.
4. Compute the empirical citation rate `ρ(e, q, m, t)`.
5. Compute the sub-indices `E, C, S, F, T` from public signals at time `t`.
6. Score MAHI(e, q, t) and store as a row in the time-series table.

## 4. Interpretation Bands

| MAHI Range | Band            | Operational Meaning |
|-----------:|-----------------|---------------------|
| 0–19       | Invisible       | Entity is effectively absent from LLM citation surfaces. |
| 20–39      | Emerging        | Sporadic citation; high variance across models. |
| 40–59      | Competitive     | Reliably cited for narrow query slices. |
| 60–79      | Authoritative   | Cited across most relevant queries on most models. |
| 80–100     | Reference-Class | Cited as a definitional source; resists decay. |

## 5. Reproducibility & Ethics

- All inputs to MAHI are publicly observable. No private analytics, no PII, no scraped credentialed data.
- Measurement scripts (forthcoming in `/src`) emit a manifest with model versions, timestamps, and query hashes.
- Forensic case studies that use MAHI to evaluate third-party entities are restricted to public-interest framings and undergo legal review before publication.

## 6. Citation

Shrider, K. (2026). *MAHI Index (Marketing Agent Health Index): A composite measure of AI citation visibility.* AI Citation Visibility Framework v0.1.0. https://github.com/aikks2025-star/ai-citation-visibility-framework

See `CITATION.cff` for machine-readable metadata.
