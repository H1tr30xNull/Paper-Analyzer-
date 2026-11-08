# Evidence & Novelty Rubrics

## Claim evidence rating (Phase 3)

| Rating | Criteria |
|---|---|
| **Strong** | Direct experiment/proof on relevant settings; fair, current baselines; multiple datasets or seeds; variance/CI or significance reported; ablation isolates the claimed cause; ideally code released or independently reproduced |
| **Moderate** | Direct evidence exists but limited: single dataset/seed, small margins without variance, some baselines missing or weak, ablation partial |
| **Weak** | Indirect or anecdotal: qualitative examples only, cherry-picked cases, evidence for a narrower claim than stated, comparison confounded (different compute/data) |
| **Unsupported** | No figure, table, proof, or citation supports it — or the evidence contradicts it |

Checks to run for each claim:
- Does the evidence test *this* claim, or a weaker/narrower one?
- Is the improvement larger than the noise (seeds, variance)?
- Are baselines tuned with comparable effort and budget?
- Does the ablation actually isolate the proposed component?
- Would the result survive a different dataset / metric / scale?

## Novelty score anchors (Phase 5)

| Score | Meaning |
|---|---|
| 1–2 | Re-application of known method with no meaningful change; or prior work already did it |
| 3–4 | Incremental: small modification, new combination of standard parts, new dataset for old method |
| 5–6 | Solid contribution: non-obvious combination or adaptation, clear gain, some new insight |
| 7–8 | Significant: new mechanism/formulation or finding that changes how a sub-area approaches a problem |
| 9–10 | Foundational: opens a new direction or overturns accepted understanding |

Always state which prior work the score was measured against. If a missing citation already
contains the core idea, cap the score accordingly and say so.

## Opportunity scoring (Phase 7)

| Metric | 1–3 | 4–6 | 7–10 |
|---|---|---|---|
| Novelty | Obvious next step many will try | Reasonable but non-trivial | Few would think of it |
| Impact | Niche improvement | Useful to a sub-community | Changes practice / broad relevance |
| Feasibility | Needs huge compute/data or unsolved prerequisites | Months of focused work | Can start this week with available resources |
| Publication potential | Workshop at best | Solid mid/top venue with good execution | Strong top-venue candidate |
