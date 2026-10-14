<!-- solve-problem:e19b7de3-fddb-4455-bfd2-bfab3666ee66 -->
# Vertex Cover below factor two

A [Tangle Solve problem](https://solve.tangle.tools/problems/e19b7de3-fddb-4455-bfd2-bfab3666ee66).

## What is the problem?

Given an undirected graph \(G=(V,E)\) with \(n\) vertices, find a minimum-cardinality vertex cover: a set \(S\subseteq V\) touching every edge. This is NP-hard. The classic greedy/matching-based 2-approximation (take both endpoints of each edge in a maximal matching) and the LP-rounding algorithm for the standard relaxation both achieve factor 2. The open question: does there exist \(\varepsilon>0\) and a polynomial-time algorithm outputting a cover of size at most \((2-\varepsilon)\cdot\mathrm{OPT}\) on **all** graphs (general Vertex Cover, not bipartite, not bounded degree)? Alternatively, prove that no such algorithm exists under an assumption strictly weaker than the Unique Games Conjecture (UGC) — e.g., NP ⊄ BPP-type assumptions, or reductions from better-studied problems. A key structural obstacle: the standard LP (min \(\sum x_v\) s.t. \(x_u+x_v\ge 1\)) has integrality gap exactly 2 (complete graph with disjoint triangles gives tightness at 2), so LP-based approaches need a stronger relaxation (e.g., SDP or Sherali–Adams/Lasserre lifts).

## Why does it matter?

Vertex Cover is arguably the most canonical NP-hard minimization problem; the factor-2 barrier is the most famous concrete gap in approximation algorithms. Breaking it (or proving it unbreakable under a weaker assumption) would either yield a genuinely new algorithmic technique or a milestone in PCP-based hardness. Integrality gaps here connect to Lasserre hierarchy power and UGC itself; progress would ripple to Max Cut, scheduling, and the broader 2-CSP approximation landscape. Practically, vertex covers model monitoring/intervention sets in network security, so even small asymptotic improvements matter heuristically.

## What's already known?

- **Algorithms:** Factor 2 is achieved by maximal matching and by LP rounding. Garg–Vempala (and later Karakostas) give \((2-\theta(1/\sqrt{\log n}))\) via semidefinite programming — a sub-2 factor but vanishing with \(n\). No fixed-\(\varepsilon\) improvement is known.
- **Hardness:** Dinur–Safra (2005) proved NP-hardness of approximating within \(1.3606-\varepsilon\) (improved slightly later to roughly 1.36 by the same line, via label cover with large alphabets and a sophisticated PCP). Khot–Regev (2008) proved that UGC implies \((2-\varepsilon)\)-hardness for every \(\varepsilon>0\).
- **Integrality gaps:** The basic LP has gap 2; integrality gap 2 (up to \(o(1)\)) persists for \(n^{\Omega(1)}\) rounds of Lasserre (Schoenebeck–Tulsiani–Trevisan-style constructions; verify exact round/count tradeoffs). Thus standard hierarchy approaches provably fail without radically new ideas.
- **UGC status:** Unresolved; recent algorithmic progress on UG itself (e.g., subexponential algorithms of Arora–Barak–Steurer) suggests UGC sits in a delicate regime.

## What would count as solving it?

Either direction closes the problem:
1. **Algorithm:** A polynomial-time algorithm and proof that it outputs a cover of size \(\le(2-\varepsilon)\cdot\mathrm{OPT}\) for some absolute constant \(\varepsilon>0\) on all graphs. Referee criterion: full proof of approximation ratio and polynomial running time.
2. **Hardness:** A reduction showing \((2-\varepsilon)\)-approximation is hard under an assumption strictly weaker/less controversial than UGC (e.g., NP-hardness at factor \(2-\delta\) for some \(\delta>0\), or hardness from \(P\ne NP\) alone via a non-UGC route). Referee criterion: gap-producing reduction with a complete soundness analysis not invoking UGC.
Intermediate wins (valuable, not full solutions): improving the Dinur–Safra constant toward 2; better Lasserre lower bounds or an algorithm beating 2 on structured graph classes.

## How to start

1. Read Dinur–Safra (2005) to understand why label-cover methods stall around 1.36 — the bottleneck is the "folding" over large alphabets and the biased-long-code analysis.
2. Read Khot–Regev (2008) to see exactly where UGC enters; note it needs only *unconditional* UG hardness of certain 2-CSPs — check whether multi-layer or "2-to-1"-flavored variants could be derandomized.
3. On the algorithmic side, study why the SDP of Garg–Vempala/Karakostas loses the \(\Theta(1/\sqrt{\log n})\): the rounding threshold analysis on the Gaussian vector. Ask whether Lasserre/HDX-inspired roundings (building on recent high-dimensional-expansion machinery) can stabilize the gain.
4. Main obstacle either way: the 2-integrality-gap instances (triangle-based) are locally indistinguishable from integrally covered graphs; any algorithm must exploit global structure the LP/SDP cannot see.

## Key references

- I. Dinur and M. Safra, "On the Hardness of Approximating Minimum Vertex Cover," *Annals of Mathematics* 162(1), 2005, pp. 439–485. Proves NP-hardness of approximating VC within \(1.3606-\varepsilon\) via a two-prover PCP with large alphabet and biased long codes.
- S. Khot and O. Regev, "Vertex Cover Might Be Hard to Approximate to Within \(2-\varepsilon\)," *J. Comput. Syst. Sci.* 74(3), 2008, pp. 335–349. Shows UGC implies \((2-\varepsilon)\)-hardness for Vertex Cover for all \(\varepsilon>0\).
- (verify) Garg, N., Vempala, S. — SDP-based \((2-\theta(1/\sqrt{\log n}))\)-approximation for Vertex Cover (conference version STOC 2004, with journal version credited to Karakostas 2005/2009).
- (verify) Schoenebeck, Tulsiani, Trevisan — Lasserre hierarchy integrality gaps of ~2 for Vertex Cover persisting for many rounds, limiting lift-and-round approaches.

## Warnings

- Do not waste time trying to fix the basic LP: the integrality gap of 2 is tight and trivial (disjoint triangles with fractional half-cover). Any LP-only approach is dead on arrival.
- "Vertex Cover" improvements exist for special cases (bipartite = exact, bounded degree, dense graphs, parameterized kernels). These do **not** address the general fixed-\(\varepsilon\) question.
- The sub-2 SDP factors in the literature shrink with \(n\); citing them as "beating 2" is a common misstatement.
- A hardness proof conditional on UGC is already known — the census asks for a *weaker* assumption, so restating Khot–Regev is not progress. Conversely, note UGC's truth is genuinely open; some researchers conjecture 2 is achievable.

---
*`ALGO-000110` · unverified*

## Acceptance guidance

Either direction closes the problem:
1. **Algorithm:** A polynomial-time algorithm and proof that it outputs a cover of size \(\le(2-\varepsilon)\cdot\mathrm{OPT}\) for some absolute constant \(\varepsilon>0\) on all graphs. Referee criterion: full proof of approximation ratio and polynomial running time.
2. **Hardness:** A reduction showing \((2-\varepsilon)\)-approximation is hard under an assumption strictly weaker/less controversial than UGC (e.g., NP-hardness at factor \(2-\delta\) for some \(\delta>0\), or hardness from \(P\ne NP\) alone via a non-UGC route). Referee criterion: gap-producing reduction with a complete soundness analysis not invoking UGC.
Intermediate wins (valuable, not full solutions): improving the Dinur–Safra constant toward 2; better Lasserre lower bounds or an algorithm beating 2 on structured graph classes.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/e19b7de3-fddb-4455-bfd2-bfab3666ee66?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000110.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000110)
