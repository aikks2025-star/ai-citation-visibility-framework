# MAHI-100 Data Directory

This directory contains the MAHI-100 prompt set (v1) and an empty capture template. It does NOT contain benchmark results. Pilot and full results, if released, will be published as separate, dated, versioned files referenced here.

## Files

- **`mahi-100-prompts-v1.csv`** — the public MAHI-100 v1 prompt set: 100 templates organized as a 10 × 10 taxonomy (10 intent buckets × 10 paraphrase variants). Each template uses a `{category}` placeholder so the benchmark is category-parametric. Contains no entity names, no scores, and no results.
- **`mahi-100-capture-template.csv`** — an empty results-capture template. Header row matches the reporting schema in [`../docs/MAHI-100.md`](../docs/MAHI-100.md) §6, plus a single, clearly fake `EXAMPLE` row showing the expected shape. This is a template, not results.

## What this directory is not

- It is **not** a completed public benchmark results corpus.
- It contains **no** scores, rankings, citation rates, named entities, or model outputs.
- The `EXAMPLE` row in the capture template is a placeholder for structure only and must not be read as data.

## How results would be released (if/when)

Any pilot or full MAHI-100 results will be published separately as dated, versioned files (for example, `results/mahi-100-run-YYYY-MM-DD.csv`) and listed here, each tied back to the same protocol and the prompt-set version used. Until such a file exists and is linked here, no MAHI-100 results have been published.

## Citation

For the methodology and prompt set, cite the AI Citation Visibility Framework concept DOI (always-latest): https://doi.org/10.5281/zenodo.20421338

Maintained by Kristina Shrider for Market Disruptors AI Visibility Agency.
