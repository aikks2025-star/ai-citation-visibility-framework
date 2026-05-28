# MAD-M: Marketing Agent Decay Model

**Author:** Kristina Shrider (ORCID: [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629))  
**Affiliation:** AI Marketing Research Institute (AIMRI); Market Disruptors Agency, Orlando, FL, USA  
**Version:** 0.1.0  
**License:** MIT (code), CC-BY 4.0 (text)

---

## 1. Purpose

The **Marketing Agent Decay Model (MAD-M)** describes how the MAHI Index of an entity changes over time in the absence of new authoritative signals. It answers the practitioner question: *"If I stop publishing, how fast do I disappear from AI citations?"*

MAD-M is a parametric decay model fit to MAHI time-series data. It is the temporal counterpart to the static MAHI Index.

## 2. Core Equation

For an entity `e` measured at times `t_0, t_1, …, t_n`, MAD-M models the MAHI trajectory as:

```
MAHI(e, t) = MAHI_floor + (MAHI_0 − MAHI_floor) · exp(−λ · (t − t_0)) + ε(t)
```

Where:

- `MAHI_0` is the score at the reference time `t_0`.
- `MAHI_floor` is the asymptotic floor (irreducible visibility from durable assets such as Wikidata QIDs and DOI-minted releases).
- `λ` is the decay rate (units: per day).
- `ε(t)` is a noise term capturing model-version churn and crawl variance.

## 3. Decay Rate Drivers

Empirically, `λ` is decomposed into four additive drivers:

```
λ = λ_index + λ_model + λ_competition + λ_canonical
```

| Driver           | Meaning |
|------------------|---------|
| `λ_index`        | Search/RAG index refresh rate — stale snapshots are dropped. |
| `λ_model`        | New model releases re-weight training data and citation priors. |
| `λ_competition`  | Competing entities publish, displacing the entity from top-N retrieval. |
| `λ_canonical`    | Canonical URL changes, broken links, or schema drift on the entity's own site. |

## 4. Half-Life

The MAHI half-life is the time required for the gap `(MAHI_t − MAHI_floor)` to halve:

```
t_half = ln(2) / λ
```

Typical empirical bands observed during framework development:

| Asset Class                        | Observed t_half |
|-----------------------------------|-----------------|
| Promotional blog post (no schema)  | 30–60 days     |
| SEO-optimized article              | 90–180 days    |
| FAQ-schema definitional page       | 180–365 days   |
| Peer-reviewed paper with DOI       | 2–5 years      |
| Wikidata QID + ORCID-anchored work | 5+ years       |

These bands are illustrative and must be re-fit for each category.

## 5. Fitting Protocol

1. Collect MAHI scores at ≥ 6 evenly-spaced timestamps spanning ≥ 90 days.
2. Estimate `MAHI_floor` from the lower envelope of the trajectory.
3. Fit `λ` and `MAHI_0` via non-linear least squares on the log-transformed gap.
4. Report `(MAHI_0, MAHI_floor, λ, t_half)` with 95% confidence intervals.
5. Cross-validate by holding out the final 20% of the series.

## 6. Operational Use

- **Content cadence planning.** Choose a publication cadence shorter than `t_half / 2` to maintain authoritative band membership.
- **Asset prioritization.** Invest in low-`λ` asset classes (DOI-minted releases, Wikidata, ORCID-anchored publications) before high-`λ` assets (promotional posts).
- **Decay alerts.** Trigger an alert when observed MAHI falls more than 1.96σ below the MAD-M-predicted value, indicating an out-of-model event (e.g., model release, competitor breakout).

## 7. Limitations

- MAD-M assumes a single dominant decay mode; multi-modal trajectories require a mixture model.
- The model treats LLM endpoints as black boxes; it does not attempt to recover internal retrieval weights.
- Decay rate estimates are sensitive to prompt phrasing; the MAHI-100 benchmark fixes prompts to reduce this source of variance.

## 8. Citation

Shrider, K. (2026). *MAD-M: Marketing Agent Decay Model for AI citation visibility.* AI Citation Visibility Framework v0.1.0. https://github.com/aikks2025-star/ai-citation-visibility-framework
