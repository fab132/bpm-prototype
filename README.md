# BPM Decision Support Prototype

Working prototype for the **Intelligent Process Automation** chapter of the
BPM group work. Implements BPMN 3 (LLM-Augmented Decision Support) using the
Anthropic Claude API.

## Files

| File | Purpose |
|------|---------|
| `bpm_decision_support.ipynb` | Main Jupyter notebook |
| `workshop_log.json` | Mock workshop log (BPMN 3 input data) |
| `governance_matrix.json` | Mock BPM Governance Matrix with 4 planted defects |
| `org_structure.json` | Mock E+H organisational structure |
| `README.md` | This file |

## Setup

1. **Install dependencies:**
   ```bash
   pip install anthropic jupyter
   ```

2. **Set your API key:**
   ```bash
   export ANTHROPIC_API_KEY=sk-ant-...
   ```
   Get a key from https://console.anthropic.com/

3. **Launch Jupyter:**
   ```bash
   jupyter notebook bpm_decision_support.ipynb
   ```

4. **Run all cells** (Cell -> Run All). Both experiments take ~10-20 seconds total.

## What the notebook does

- **Section 1-3:** Setup, data loading, core `decision_support()` function.
- **Section 4 (Experiment 1):** Framework Review — NVA step, full delegation.
  Asks the LLM to rank three governance frameworks for E+H.
  Validation: compare ranking against the case-study verdict.
- **Section 5 (Experiment 2):** RACI Conflict Detection — BVA step.
  Asks the LLM to audit the (deliberately flawed) governance matrix.
  Validation: recall on 4 planted defects, false-positive count.
- **Section 6:** Cost-benefit summary with API token costs.
- **Section 7:** Conclusion.

## Planted defects in `governance_matrix.json`

These are intentional and serve as ground truth for Experiment 2:

1. **Duplicate Accountable / Responsible** on "Ensure cross-functional
   communication" — RACI rule violation.
2. **Missing Responsible** (`null`) on "Periodic governance matrix review".
3. **Misplaced Consult** — Quality Management on "IT-related process
   changes review".
4. **Missing Inform path** — "End-to-end value optimization" has no Sales
   or Marketing in the Inform column.

## Cost

Both experiments combined consume ~10k input tokens and ~2k output tokens,
costing roughly **USD 0.05-0.08** at current Sonnet 4.5 pricing.

## For the appendix

Screenshot recommendations:
- The Experiment 1 output cell (top choice + ranking).
- The Experiment 2 output cell (detected defects with severity).
- The validation cell showing 100% recall on planted defects.
- The cost-benefit summary table at the bottom.
