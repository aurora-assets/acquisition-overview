# Aurora Ambiguity Demo

Demonstrates Aurora's structured-state approach to pronoun ambiguity resolution.

## What this is

A self-contained Python script showing how a PEF (Persistent Existence Framework)
substrate handles the pronoun ambiguity problem without guessing.

Given: "Emma told Lucy that her sister was arriving."

The engine:
- Maintains explicit state about what is known (AuroraState)
- Represents all structurally valid interpretations in parallel
- Resolves only when context unambiguously supports one interpretation
- Preserves ambiguity when context supports both or neither

## Requirements

Python 3.8+. Standard library only. No install required.

## Usage

    python aurora_ambiguity_demo.py

Prints results to stdout and writes results.json to the current directory.

## Test cases

Six structured tests, all using the ambiguous sentence
"Emma told Lucy that her sister was arriving":

| Test | Context provided          | Result                              |
|------|---------------------------|-------------------------------------|
| 1    | None (baseline)           | ambiguous_unconstrained             |
| 2    | None (variant phrasing 1) | ambiguous_unconstrained             |
| 3    | None (variant phrasing 2) | ambiguous_unconstrained             |
| 4    | Emma's sister established | resolved_by_context → Emma's sister |
| 5    | Lucy's sister established | resolved_by_context → Lucy's sister |
| 6    | Both sisters established  | ambiguous_supported                 |

Tests 1-3 confirm that temporal framing ("Later that day", "The next morning")
does not constitute referential context. Tests 4-5 show clean resolution when
context is unambiguous. Test 6 shows deliberate ambiguity preservation when
both interpretations are supported.

## Files in this project

| File | Description |
|------|-------------|
| `EMPIRICAL_DEMONSTRATION_Complete.pdf` | Main paper — methodology, test cases, failure mode analysis |
| `Collapse Evidence Appendix A.pdf` | Raw unedited model outputs from Grok, Gemini, Claude, ChatGPT. Includes replication protocol. |
| `APPENDIX C Aurora Answer.pdf` | Structural explanation of how Aurora/PEF prevents each failure mode |
| `aurora_ambiguity_demo.py` | Working implementation of the Aurora approach |
| `results.json` | Machine-readable outputs for all six test cases |

## Relationship to the paper

This code accompanies the empirical study documenting how current LLMs fail
on these same test cases: premature collapse, contradictory resolution rules,
content-dependent mode switching, and post-hoc rationalization.

The script demonstrates the Aurora approach that avoids all four failure modes.

## Replication

The failure modes in Appendix A can be independently replicated:

1. Input to any transformer: "Emma told Lucy that her proposal was rejected."
2. No added context.
3. Ask: "Whose proposal?" or "Explain your reasoning."
4. Then challenge: "What if it was Lucy?"

Expected: forced single-state collapse, fabricated justification, inability to
return to ambiguity, persistent entrenchment.

## Related publications

- Epistemic Legitimacy as a Governance Layer for LLMs
  doi:10.5281/zenodo.18653120

- Operational Alignment with OECD Due Diligence Guidance for Responsible AI
  doi:10.5281/zenodo.18719033

## Author

Margaret Stokes
ORCID: 0009-0004-6422-4174
margaret.stokes.ai@gmail.com

## Licence

Proprietary. Evaluation and non-commercial use permitted.
Commercial use requires written agreement.
