# Aurora Governance Stack — Acquisition Overview

This organisation holds the complete IP asset bundle for Aurora: a deterministic governance layer for LLMs that enforces admissibility at inference time and produces cryptographically verifiable audit records.

## Code Repositories

| Repo | Description |
|------|-------------|
| [aurora-lens](../aurora-lens) | Provider-agnostic governance proxy. Sits between your application and the LLM, enforcing admissibility decisions at inference time with hash-chained forensic audit output and streaming support. Published on PyPI. |
| [aurora-governor](../aurora-governor) | The governance kernel. Implements 28 verifier invariants and a STOP/CLARIFY/REFUSE/ADMIT decision engine with AFL-JSONL-1 forensic ledger output. |
| [Aurora-PEF](../Aurora-PEF) | Persistent Existence Framework. A meaning-first reasoning substrate grounded in conceptual topology and persistent entity representation. |

## IP Documentation

### 01 — Governance IP
Specifications and research underlying the governance architecture.

### 02 — Reasoning Architecture
Formal documents covering conceptual geometry, compositional primitives, derivation methods, and executable block specifications.

### 03 — Empirical Evidence
Structured demonstration of LLM failure modes in ambiguity resolution, with cross-platform test protocol and full reproducibility materials.

## PyPI

`aurora-lens` is available as a Python package:

```
pip install aurora-lens
```

https://pypi.org/project/aurora-lens/

## Patent Position

Five provisional applications were filed with IP Australia between November and December 2025. Non-provisional filings are due November–December 2026. Full specifications are available under NDA.

## Published Research

- doi:10.5281/zenodo.18653120 — Epistemic Legitimacy as a Governance Layer for LLMs: Architecture and Implementation
- doi:10.5281/zenodo.18719033 — Operational Alignment of Aurora-Lens with OECD Due Diligence Guidance for Responsible AI (2026)
- ORCID: 0009-0004-6422-4174

## Contact

Margaret Stokes
margaret.stokes.ai@gmail.com
https://milamba.com/aurora-lens.html
