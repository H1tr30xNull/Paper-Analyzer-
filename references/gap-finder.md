# Research Gap Finder Mode (multiple papers)

Use when the user provides several papers or asks for gaps across a topic.

## Steps

1. **Per-paper pass** (lighter depth): problem, method, datasets/benchmarks, headline
   claims + evidence rating, stated limitations. Put them in one comparison table:

   | Paper | Year | Problem | Method family | Data / benchmark | Key claim | Evidence | Limitations |
   |---|---|---|---|---|---|---|---|

2. **Expand the set** if it's small or biased: search recent (12–24 months) and highly
   cited related work so the maps reflect the field, not just the user's selection.
   Mark which papers were user-provided vs added.

3. **Build the five maps:**

### Consensus Map
What most papers agree on (findings, assumptions, evaluation practices). Note how many
papers and whether agreement is independent or one lab/benchmark echoed.

### Contradiction Map
Where papers disagree — conflicting results, opposite conclusions, incompatible
assumptions. For each: papers on each side, likely cause (setup, data, metric, scale),
and what experiment would resolve it.

### Saturation Map
Overcrowded areas: many papers, small marginal gains, saturated benchmarks. Signals:
leaderboard deltas < noise, same benchmark reused everywhere, many near-identical methods.

### Blind Spot Map
Neglected areas: settings, populations, languages, scales, failure modes, evaluation
dimensions (cost, robustness, fairness, latency), or method families nobody tried.

### Opportunity Map
Concrete directions derived from the other four maps (contradictions to resolve, blind
spots to fill, saturated areas to leave). Rank with the 1–10 scores
(Novelty · Impact · Feasibility · Publication Potential).

## Visualization (optional)
A 2D grid (e.g. method family × setting) with paper counts per cell makes saturation and
blind spots obvious at a glance — empty cells are candidate gaps.
