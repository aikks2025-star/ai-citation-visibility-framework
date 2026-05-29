# MAD-M: Marketing Agent Decay Model

**Author:** Kristina Shrider (ORCID: [0009-0002-2655-4629](https://orcid.org/0009-0002-2655-4629))  
**Affiliation:** AI Marketing Research Institute (AIMRI); Market Disruptors Agency, Orlando, FL, USA  
**Version:** 0.2.1  
**License:** MIT (code), CC-BY 4.0 (text)

---

## 1. Purpose

The **Marketing Agent Decay Model (MAD-M)** is a governance-first heuristic and planning lens for how AI-mediated marketing systems can lose visibility, attribution, and authority over time when freshness, sourcing, differentiation, and human review are left unmanaged.

MAD-M answers the practitioner question: *"What unmanaged decay risks should we plan for before our content silently loses AI visibility?"*

MAD-M is not a prediction engine, traffic forecast, ranking guarantee, or fixed timeline. It is the temporal governance companion to the MAHI Index. MAHI diagnoses current AI visibility health; MAD-M helps teams plan content review, refresh, provenance, and citation-maintenance cycles.

## 2. Core Equation

For an entity `e` measured at times `t_0, t_1, …, t_n`, MAD-M can be represented as a conceptual decay curve:

```
MAHI(e, t) = MAHI_floor + (MAHI_0 − MAHI_floor) · exp(−λ · (t − t_0)) + ε(t)
```

Where:

- `MAHI_0` is the score at the reference time `t_0`.
- `MAHI_floor` is the asymptotic floor (irreducible visibility from durable assets such as Wikidata QIDs and DOI-minted releases).
- `λ` is a conceptual decay pressure term, not a guaranteed observed rate.
- `ε(t)` is a noise term capturing model-version churn, crawl variance, and retrieval variance.

This equation is a planning abstraction. It should not be used to promise a specific ranking, traffic, or citation outcome.

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

## 4. The 12-Week Drift Scenario

The MAD-M 12-week drift scenario is a core planning lens for operational teams. It shows how unmanaged AI-assisted content can move from early freshness to lower retrievability if the asset is not refreshed, sourced, differentiated, and governed.

The 12-week scenario is **not** a guaranteed prediction, ranking forecast, or fixed traffic timeline. It is a heuristic for planning review cycles.

| Phase | Timing | Risk State | Description |
|-------|--------|------------|-------------|
| Freshness Advantage | Weeks 1-2 | Optimal | Newly published or refreshed content may benefit from novelty, recency, and early engagement signals. |
| Pattern Recognition | Weeks 3-4 | Caution | Engagement normalizes and systems may begin detecting repeated structures, generic phrasing, or weak differentiation. |
| Confidence Erosion | Weeks 5-6 | Caution | Trust and relevance signals soften unless the page contains original differentiation, first-party observations, primary sources, and clear provenance. |
| Authority Decay | Weeks 7-8 | High Risk | Competing sources that are fresher, better sourced, or more strongly corroborated can begin taking citation share and organic reach. |
| Systemic Deprioritization | Weeks 9+ | Critical | The asset may enter a persistent low-priority state where light edits are not enough; recovery may require structural changes, stronger sourcing, clearer entity signals, new corroboration, or repositioning. |

Operationally, MAHI is used to diagnose current visibility health, while the MAD-M 12-week scenario is used to plan governance and content refresh cycles before visibility loss becomes difficult to reverse.

## 5. Half-Life

The MAHI half-life is the time required for the gap `(MAHI_t − MAHI_floor)` to halve:

```
t_half = ln(2) / λ
```

Illustrative planning bands:

| Asset Class                        | Observed t_half |
|-----------------------------------|-----------------|
| Promotional blog post (no schema)  | 30–60 days     |
| SEO-optimized article              | 90–180 days    |
| FAQ-schema definitional page       | 180–365 days   |
| Peer-reviewed paper with DOI       | 2–5 years      |
| Wikidata QID + ORCID-anchored work | 5+ years       |

These bands are illustrative only. They must not be treated as universal benchmarks, guarantees, or forecasts.

## 6. Measurement Protocol

1. Collect MAHI scores at >= 6 evenly-spaced timestamps spanning >= 90 days.
2. Estimate `MAHI_floor` from the lower envelope of the trajectory.
3. Estimate `λ` and `MAHI_0` as planning parameters, not guaranteed future rates.
4. Report `(MAHI_0, MAHI_floor, λ, t_half)` with 95% confidence intervals.
5. Cross-validate by holding out the final 20% of the series.

## 7. Operational Use

- **Governance planning.** Use the 12-week scenario to schedule source reviews, content refreshes, and provenance checks.
- **Content cadence planning.** Choose a review cadence shorter than the expected decay window for the asset class.
- **Asset prioritization.** Invest in low-`λ` asset classes (DOI-minted releases, Wikidata, ORCID-anchored publications) before high-`λ` assets (promotional posts).
- **Decay alerts.** Trigger review when observed MAHI falls materially below the expected range, indicating a possible model release, competitor breakout, source loss, or canonical drift event.

## 8. Limitations

- MAD-M assumes a single dominant decay mode; multi-modal trajectories require a mixture model.
- The model treats LLM endpoints as black boxes; it does not attempt to recover internal retrieval weights.
- Decay rate estimates are sensitive to prompt phrasing; the MAHI-100 benchmark fixes prompts to reduce this source of variance.
- The 12-week drift scenario is a planning heuristic, not a universal timeline. Some assets decay faster, some slower, and DOI-backed or knowledge-graph-supported assets can remain durable far longer.

## 9. Citation

Shrider, K. (2026). *MAD-M: Marketing Agent Decay Model for AI citation visibility.* AI Citation Visibility Framework. https://doi.org/10.5281/zenodo.20421338
