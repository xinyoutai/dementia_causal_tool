# DEMON Network — Causal Evidence Grading Tool

**File:** `DEMON_Grading_Tool.html`
**Version:** Draft (March 2026)
**Context:** Companion tool for the manuscript *"Assessing whether dementia risk factors are causal: a DEMON Network consensus framework for evidence grading"*

---

## What it does

A single-page web application that walks a researcher through a structured assessment of whether a putative dementia risk factor is likely causal. The user evaluates five evidence domains, and the tool computes an overall causal evidence grade.

---

## How to use it

1. Open `DEMON_Grading_Tool.html` in any modern browser (no server, installation, or internet connection required).
2. Enter the name of the risk factor you are assessing.
3. Work through five domain panels (A–E) in order. For each domain:
   - Read the sub-criteria and tick those that are met by the current evidence base.
   - The tool will suggest a domain rating based on your ticks (indicated by a pulsing highlight and "suggested" label).
   - Select a rating: **Strong**, **Moderate**, **Weak**, or **Contradictory**. You can override the suggestion.
   - If you override, a "Show suggested rating" button appears so you can reconsider.
4. After completing all five domains, the Summary panel displays your results.

---

## The five domains

| Domain | What it assesses | Sub-criteria |
|--------|-----------------|--------------|
| **A — Robustness of Association and Bias Control** | Is the association replicated, consistent, and not explained by confounding? | A1. Replication breadth (≥3 cohorts, ≥2 populations); A2. Effect size consistency (I² < 50%); A3. Confounding robustness (methods beyond standard adjustment) |
| **B — Temporality and Reverse Causation** | Is the temporal direction established and reverse causation by prodromal dementia addressed? | B1. Long lag analysis (≥10-year lag, effect persists); B2. Prodromal case exclusion (≥5-year window or biomarker-based); B3. Temporal dose-response (earlier/longer exposure → higher risk) |
| **C — Biological and Mechanistic Coherence** | Is there a plausible biological pathway to neurodegeneration or cerebrovascular pathology? | C1. Identified human pathway (neuropathology, neuroimaging, biomarkers); C2. Cross-species or in-vitro corroboration |
| **D — Experimental and Quasi-Experimental Evidence** | Do designs that mitigate confounding by design support a causal effect? | D1. RCT evidence (adequate power, dementia incidence or validated cognitive outcome); D2. Mendelian randomisation (F > 10, pleiotropy-robust methods); D3. Natural experiment or target trial emulation |
| **E — Triangulation Across Designs** | Do methodologically diverse designs with non-overlapping biases converge? | E1. Design diversity (≥3 distinct designs); E2. Convergence across complementary bias structures |

---

## The four rating levels

| Rating | Colour | Meaning |
|--------|--------|---------|
| **Strong** | Green | All (or nearly all) sub-criteria for the domain are met |
| **Moderate** | Amber | Most sub-criteria met, or all partially met |
| **Weak** | Red | An evidence gap — insufficient studies exist to assess the domain. This is absence of evidence, not evidence of absence |
| **Contradictory** | Black | Active evidence against the causal direction for this domain |

The critical distinction is between **Weak** (we don't have enough data — a research priority problem) and **Contradictory** (we have data and it points the other way — an inferential problem).

---

## Auto-suggestion logic

The tool suggests a rating based on ticked sub-criteria. It never auto-suggests "Contradictory" — that always requires active judgment from the rater.

| Domain type | All ticked | Most ticked | Few/none ticked |
|-------------|-----------|-------------|-----------------|
| 3-criteria domains (A, B, D) | Strong | Moderate (2 of 3) | Weak (0–1 of 3) |
| 2-criteria domains (C, E) | Strong | Moderate (1 of 2) | Weak (0 of 2) |

---

## Grade mapping rules

The five domain ratings are mapped to an overall grade via explicit rules, checked in this order:

1. **Disease Marker** (checked first): Triggered if Domain B or Domain D is rated Contradictory. Interpretation — the association is more consistent with the exposure being a consequence of preclinical neuropathology than a cause.
2. **Grade I — Strong Evidence for Causality:** ≥4 domains Strong, including B and E; no Contradictory ratings. Interpretation — high confidence that modifying this exposure would alter dementia risk.
3. **Grade II — Probable Causal Effect:** All domains Strong or Moderate; ≥2 Strong; either B or D must be Strong; no Contradictory. Interpretation — likely causal, further triangulation needed.
4. **Grade IV — Insufficient Evidence** (checked before III): ≥3 domains rated Weak. Interpretation — too sparse to draw conclusions.
5. **Grade III — Possible Causal Effect:** ≥3 domains Strong or Moderate; ≤1 Contradictory. Interpretation — plausible but genuinely uncertain.

If no rule matches, defaults to Grade IV.

---

## Summary panel output

After completing all domains, the tool generates:

- A **five-domain profile grid** showing each domain's rating with colour coding
- The **overall grade** with its interpretation
- A **narrative summary statement** describing the evidence profile in prose
- An **evidence gaps list** identifying every non-Strong domain with the specific scoring rule that was not met

---

## Technical details

- Pure HTML/CSS/JavaScript — no dependencies, no build step, no server
- Works offline in any modern browser
- Responsive layout (adapts to mobile screens)
- Sticky progress bar with clickable navigation between completed panels
- Collapsible scoring rules per domain
- All state held in memory — nothing is saved or transmitted. Refresh clears the assessment.
