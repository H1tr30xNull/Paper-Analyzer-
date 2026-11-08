---
name: paper-analyzer
description: Analyze a research paper as a researcher, not a reader — contributions, evidence strength per claim, related-work positioning, novelty score, critical review, and ranked research opportunities. Use whenever the user shares or names a paper (PDF, arXiv/OpenReview/DOI link, title) and wants to understand, review, critique, reproduce, implement, position, or build on it — e.g. "đọc paper này", "analyze this paper", "review this paper", "is this paper any good", "what's novel here", "what can I research next from this", "literature review", "find research gaps" — even if they don't say "analyzer". With multiple papers, runs Research Gap Finder mode (consensus / contradiction / saturation / blind-spot / opportunity maps).
---

# Paper Analyzer

## Purpose

Most paper-reading answers *"What does the paper say?"*
This skill answers:

- **Why does the paper matter?**
- **How much should I trust it?**
- **How does it compare to related work?**
- **What should I do next?**

Summarizing is the easy 20%. The value is in judging evidence, positioning the paper
against the field (including work published *after* the model's training data or the
paper itself), and extracting concrete next research moves.

Throughout, keep two voices clearly separate: **what the authors claim** vs **what the
analysis concludes**. Mixing them is the main way paper analyses mislead people.

---

## Phase 1 — Context Acquisition

Before reading the paper, understand the reader.

**User context** — determine (infer from the conversation when possible; ask briefly only
if it changes the analysis):
- Why they're reading it and their current project / research objective
- Their domain expertise (sets how much background to explain)
- Desired output — one of: *Understanding · Literature Review · Implementation ·
  Reproduction · Paper Review (reviewer-style) · Research Gap Discovery · New Research Direction*

The goal changes emphasis: Implementation → algorithms, hyperparameters, code availability;
Paper Review → evidence & fairness; Gap Discovery → Phases 4, 7 weigh most.

**Workspace context** — inspect what's around: PDFs, notes, source code, datasets, related
documents in the working directory (list them). Read what's relevant — never assume a file
was read because it exists.

Produce a short **Research Context Map**: user goal, expertise, project, relevant local
artifacts (read / skimmed / not read), and what the analysis should optimize for.

---

## Phase 2 — Deep Paper Reading

Get the full text. PDF → read all pages (use the PDF skill or Read with page ranges for
long files); link → fetch the paper itself (arXiv abs → PDF/HTML, OpenReview, ACL Anthology,
DOI). Also check for an official code repo, project page, and — if on OpenReview — the
reviews and author responses, which are often the best critical signal available.

Read **all** of: title, abstract, introduction, methodology, experiments, limitations,
appendices, references. Appendices often hide the real hyperparameters, failed settings,
and caveats; the reference list is the starting point for Phase 4.

Extract:

| Item | Content |
|---|---|
| Problem | What exactly is being solved |
| Motivation | Why it matters / what's wrong with existing approaches |
| Assumptions | Stated *and* implicit (data, compute, setting, distribution) |
| Methodology | Core idea in 2–3 sentences, then the mechanism |
| Experiments | Datasets, baselines, metrics, ablations, compute |
| Results | Headline numbers with context (vs which baseline, by how much) |
| Contributions | As the authors list them |

---

## Phase 3 — Evidence Mapping

For **every major claim** (contributions + headline results + any "we show that…"),
find its supporting evidence: which experiment, figure, table, metric, and any
statistical evidence (seeds, variance, confidence intervals, significance tests).

Rate each claim using `references/evidence-rubric.md`:
**Strong · Moderate · Weak · Unsupported**

Output a Claim → Evidence table. A claim with no figure/table/proof behind it is
*Unsupported* no matter how confidently it's written.

---

## Phase 4 — Related Work Analysis

This is what differentiates the analysis. Don't rely only on the paper's own related-work
section — authors choose what to compare against. **Search** (Semantic Scholar, Google
Scholar, arXiv, OpenReview, Papers with Code, ACL Anthology, DBLP, Connected Papers-style
citation graphs; the `reconnaissance` skill's approach works well here) for:

- **Foundational papers** — what this work builds on
- **Competing papers** — alternative approaches to the same problem
- **State-of-the-art** — current strongest methods/results on the same benchmarks
- **Recent papers** — latest developments, focusing on the **last 12–24 months** when
  applicable, including work that cites this paper (follow-ups, rebuttals, reproductions)

For each related paper note: what it does, how it relates (builds on / competes / supersedes /
contradicts), and whether this paper cites it. Cite with links.

---

## Phase 5 — Novelty Assessment

Only after Phase 4 — novelty can't be judged without searching recent literature.

Classify components:
- **Truly novel** — ideas not found in prior work
- **Incremental improvements** — refinements of existing ideas
- **Reused components** — established techniques (name the origin)
- **Missing citations** — relevant prior/concurrent work not discussed (and whether it weakens the novelty claim)

Give a **Novelty Score 1–10** with a one-paragraph justification (anchors in
`references/evidence-rubric.md`).

---

## Phase 6 — Critical Review

Question every major claim. Look for:

- **Hidden assumptions** — what has to be true for the method to work
- **Weaknesses** — conceptual and empirical
- **Failure modes** — where it would break (scale, distribution shift, adversarial, edge cases)
- **Benchmark biases** — saturated/contaminated benchmarks, cherry-picked datasets or metrics
- **Reproducibility risks** — missing code/hyperparameters/seeds, huge compute, private data
- **Missing experiments** — ablations, baselines, scales, or settings that should be there
- **Unfair comparisons** — tuned method vs untuned baselines, different compute/data budgets, outdated baselines

Also list genuine **strengths** — a fair review credits what's done well.

---

## Phase 7 — Research Opportunity Discovery

Every paper should yield **at least one** research opportunity. Generate:

- Open questions · Missing evaluations · Alternative methodologies ·
  Unexplored applications · Contradictions (with other work) · Research gaps

Make each one concrete: what to do, why it's open, a first experiment.
Rank in a table scored 1–10 on **Novelty · Impact · Feasibility · Publication Potential**
(plus total). Tailor feasibility to the user's resources if known.

---

## Phase 8 — Researcher Deliverables

Write the report using `references/output-template.md`:

1. **Executive Summary** — one page max
2. **Contribution Summary**
3. **Evidence Assessment** — claim → evidence → rating
4. **Novelty Analysis** — novel vs incremental vs reused, score
5. **Related Work Positioning** — where it sits in the field
6. **Critical Review** — strengths & weaknesses
7. **Research Opportunities** — ranked

Scale to the user's goal: for "just help me understand it" keep Phases 3–7 compact but
still present; for a review or gap discovery go full depth.

**Output location:** with a filesystem, save to `paper-analysis/<paper-slug>.md` and give a
short chat summary with the path; otherwise deliver in chat. Write prose in the user's
language; keep technical terms, paper titles and quotes in the original.

---

## Optional Mode — Research Gap Finder (multiple papers)

When the user gives several papers (or asks for gaps across a topic), run Phases 2–3
per paper at a lighter depth, then build the five maps described in
`references/gap-finder.md`: **Consensus · Contradiction · Saturation · Blind Spot · Opportunity**.

---

## Principles

- Never trust author claims without evidence.
- Distinguish author claims from analyzer conclusions.
- Compare against related work whenever possible.
- Identify what is missing, not only what is present.
- Search recent literature before assessing novelty.
- Every paper should produce at least one research opportunity.
- Reading is the beginning; insight extraction is the goal.
