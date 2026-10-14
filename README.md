<!-- solve-problem:5d404ee6-e1fb-47de-a1be-70f32aa15a1a -->
# Strongly explicit optimal Ramsey graphs

A [Tangle Solve problem](https://solve.tangle.tools/problems/5d404ee6-e1fb-47de-a1be-70f32aa15a1a).

## What is the problem?

Construct, for every \(N\), an (undirected) graph \(G_N\) on \(N\) vertices such that:

1. **Ramsey property:** \(G_N\) contains no clique and no independent set of size larger than \(C\log N\), for an absolute constant \(C\) (random graphs achieve this with \(C \approx 2/\log 2 \approx 2.88\) for the relevant \(R(k,k) > N\) threshold; any universal constant is acceptable).
2. **Strong explicitness:** the \(i\)-th vertex is labeled by a \(\log N\)-bit string, and adjacency of \(i, j\) is computable by a deterministic algorithm running in time \(\mathrm{poly}(\log N)\) — i.e., exponentially faster than reading the graph, which has \(\Theta(N^2)\) edges.

Ambiguity to note: "optimal" means order-\(\log N\) (matching Erdős's probabilistic bound up to the constant), not any specific constant. Some literature weakens (1) to \(2^{O(\log\log N)^2}\) or \(N^{o(1)}\); those are strictly easier and do **not** solve this problem. The gold standard also sometimes asks for \(O(\log N)\) or even \(O(\log N / \log\log N)\); here \(O(\log N)\) suffices.

## Why does it matter?

This is a flagship "derandomization of the probabilistic method" problem: it asks to make the most famous existence proof in combinatorics constructive. Success would represent the first derandomization of a result where the probabilistic argument works at essentially tight parameters — a landmark for pseudorandomness. Ramsey graphs serve as universal tools: they yield explicit two-source extractors, dispersers, and lower bounds in communication complexity and proof complexity. Failure to close the gap is a key datapoint on the limits of the "conditional pseudoentropy / extractor" program.

## What's already known?

- **Probabilistic bound (Erdős 1947):** a random graph on \(N\) vertices has no clique/independent set larger than \(\sim 2\log_2 N\), so \(R(k,k) > 2^{k/2}\).
- **Historical explicit line:** Frankl–Wilson, and the Gopalan–Mergo–Reingold–Yehudayoff survey, gave \(N\)-vertex graphs with \(2^{O(\sqrt{\log N}\log\log N)}\) and later \(2^{O(\log\log N)^2}\) "bad set" size — far from \(\log N\).
- **Extractor breakthrough:** Chattopadhyay–Zuckerman (2016), via Chattopadhyay's earlier Ramsey-type constructions, connected this to two-source extractors; Cohen (2016) and Li (2017, 2023; arXiv:2303.06802) improved this to \(2^{(\log\log N)^{O(1)}}\)-type bounds (polylogarithmic in the bad-set parameter after normalization), still not \(O(\log N)\).
- **Barriers:** current extractor-based constructions rely on non-malleable or correlated-sample extractors whose error necessarily polylog factors; no known technique converts a min-entropy \(n/2\), \(O(1)\)-error two-source extractor into the \(1/N\)-type error needed for \(O(\log N)\) Ramsey sets.

## What would count as solving it?

- **Upper bound (the problem):** an explicit family \(G_N\) with \(\omega(G_N), \alpha(G_N) \le C\log N\) and adjacency computable in \(\mathrm{poly}(\log N)\) time, with proof. Matching Erdős's constant \(2+o(1)\) would be stronger but is not required.
- A hardness route also counts conceptually: prove that any polynomial-time computable graph family must have clique or independent set \(\omega(\log N)\) (currently wide open; no nontrivial lower bound for explicit graphs is known).
- Partial credit milestones: \(O(\log N \cdot \mathrm{polyloglog} N)\), or \(O(\log N)\) with quasipolynomial-time adjacency.

## How to start

1. Read the Gopalan–Mergo–Reingold–Yehudayoff survey "Finding the right source: extracting from random walks" no — read their survey **"Deterministic construction of Ramsey graphs"** (or equivalently Chapter on Ramsey graphs in Goldreich's newer textbook) for the pre-2016 landscape and the Frankl–Wilson–Grolmusz approaches.
2. Read Chattopadhyay–Zuckerman (STOC 2016, "Explicit two-source extractors with resilient error") and Li's arXiv:2303.06802 to understand the current extractor→Ramsey reduction; identify exactly where the loss from \(\log N\) to \((\log\log N)^{O(1)}\) enters (it is the error/seed length of the component extractors).
3. Main obstacle: obtaining a two-source extractor with min-entropy \(n/2\), error \(N^{-\Omega(1)}\), and negligible overhead — known constructions have error only \(2^{-\mathrm{polylog}}\). Try improving error via seeded-merging (Li's technique) or non-malleable extractors with amortized seed reuse.
4. Alternative: bypass extractors via algebraic/combinatorial designs (Frankl–Wilson style with prime-power moduli) or communication-complexity lower-bound constructions (e.g., ramsey graphs from set-disjointness — the "pseudoentropy" idea of Chattopadhyay's earlier work).

## Key references

- P. Erdős, "Some remarks on the theory of graphs," *Bull. AMS* 53 (1947). The probabilistic method's birthplace: shows random graphs on \(N\) vertices have clique/independent sets \(\le 2\log_2 N\).
- E. Chattopadhyay, D. Zuckerman, "Explicit two-source extractors with resilient error," STOC 2016. Breakthrough converting two-source extractors into explicit Ramsey graphs with \(2^{O((\log\log N)^2)}\) bad sets.
- X. Li, "Two source extractors for affine non-oblivious bit-fixing sources, and explicit Ramsey graphs," arXiv:2303.06802 (2023). Current best explicit Ramsey bound via improved extractors. https://arxiv.org/abs/2303.06802
- G. Cohen, "Making the most of advice: New correlation breakers and related applications," STOC 2016. Improved the CZ line to \(2^{O(\log\log N)}\)-type bounds. (verify exact parameter statement)
- O. Goldreich, *Introduction to Property Testing / lecture notes* — contains a chapter surveying explicit Ramsey graph constructions. (verify)

## Warnings

- Terminology trap: papers saying "explicit optimal Ramsey graphs" sometimes mean optimal up to \(N^{o(1)}\), not \(\Theta(\log N)\). Always check the exact bound.
- "Strongly explicit" (poly(log N) adjacency) is strictly harder than "explicit" (poly(N)); constructions output by poly-time algorithms counting \(N\) as input length don't automatically qualify.
- Don't conflate \(O(\log N)\) with the conjectured truth \(O(\log N)\) being tight for random graphs — achievability, not constant-matching, is the target.
- The extractor route has an intrinsic-looking error bottleneck; several groups have failed there. Consider genuinely different constructions (rank/communication complexity) before grinding on extractor parameters.
- Citation details marked "(verify)" above should be checked before relying on them.

---
*`ALGO-000057` · flagged for review*

## Acceptance guidance

- **Upper bound (the problem):** an explicit family \(G_N\) with \(\omega(G_N), \alpha(G_N) \le C\log N\) and adjacency computable in \(\mathrm{poly}(\log N)\) time, with proof. Matching Erdős's constant \(2+o(1)\) would be stronger but is not required.
- A hardness route also counts conceptually: prove that any polynomial-time computable graph family must have clique or independent set \(\omega(\log N)\) (currently wide open; no nontrivial lower bound for explicit graphs is known).
- Partial credit milestones: \(O(\log N \cdot \mathrm{polyloglog} N)\), or \(O(\log N)\) with quasipolynomial-time adjacency.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/5d404ee6-e1fb-47de-a1be-70f32aa15a1a?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000057.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000057)
