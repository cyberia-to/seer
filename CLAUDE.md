# seer — agent instructions

seer proposes cyberlinks; tru measures them. read README.md first — the two invariants there are the whole boundary:

1. nothing in this repo computes φ* or touches tru's focusing iteration. learning lives outside the contraction.
2. every proposal objective is the neuron's expected settlement under tru/specs/rewards.md. structural signals (Δλ₂, articulation points) are priors, never the reward.

## layout

- `specs/` — contracts (interface, densification). source of truth; when code and spec disagree, fix the spec first, then propagate.
- `docs/` — why seer exists. explains, never restates the specs.
- `roadmap/` — proposals with `status:` frontmatter (proposal → accepted → in spec). rejected proposals stay for rationale.

## conventions

- pages are markdown with YAML frontmatter; wiki-links `[[page]]` resolve across the cyber graph. never write `[[term]]s` — put plurals in `alias:`.
- no bold in graph pages. state what a thing is; never define by negation.
- commit by default, atomic, conventional prefixes (`feat:`, `fix:`, `docs:`, `chore:`).
- fixed-point over the Goldilocks field wherever a number must agree across machines (see tru/specs/arithmetic.md). anything seer computes privately for ranking may use floats; anything it publishes as a claim may not.

## companion repos

| repo | seer reads | seer writes |
|---|---|---|
| tru | φ*, cyberank, Δφ⁺ marginal, λ₂, spectral positions, syntropy | nothing |
| cybergraph | signals, cyberlinks, particles | nothing directly — proposals go to the neuron |
| cyb | the neuron's keys, will, context | candidate signals for the owner to sign |
