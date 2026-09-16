---
title: seer
tags: cyber, cyb, seer, core
crystal-type: entity
crystal-domain: cyber
icon: "🔮"
alias: seer, cyber-seer, cyber/seer, the proposer, link proposal
---
# seer

seer answers one question for a [[neuron]]: what should I link next?

[[tru]] measures the [[cybergraph]] — it computes [[focus]] $\phi^*$, the impulse $\Delta\phi^+$ a link delivers, the spectral gap $\lambda_2$, the spectral positions of every particle, and what a link will settle for. tru is deterministic by contract and never decides what to link. seer is the mind that acts on the measure: it reads tru's outputs and the graph, proposes candidate [[cyberlinks]], and hands them to the neuron to sign. it runs on the neuron's side — inside the robot ([[cyb]]), inside the protocol's own agency ([[cyber/self/linking|self/linking]]), or inside any agent with a key.

two invariants hold the boundary:

1. seer never computes $\phi^*$ and never touches the [[focusing]] iteration. learning lives here, outside the contraction, so tru stays bit-identical on every machine.
2. seer optimizes the neuron's own expected settlement under [[rewards]] — the surprise-gated $\Delta\phi^+$ the protocol actually pays — with structural signals as priors. a proposer trained on a bespoke score would propose links that do not pay.

## methods

| method | kind | signal | status |
|---|---|---|---|
| [densification](specs/densification.md) | analytical | Fiedler vector → $\Delta\lambda_2$ per link, three phases (bridge → mesh → semantic) | specified, unbuilt |
| [learned proposal](roadmap/learned-proposal.md) | learned | GFlowNet sampling links in proportion to expected settlement, densification as teacher | proposal |

## map

- [specs/interface.md](specs/interface.md) — the contract: what seer reads from tru and the graph, what it emits, what it must not do
- [specs/densification.md](specs/densification.md) — cyber-seer, the analytical method
- [docs/link-production.md](docs/link-production.md) — why: link production is the intelligence problem the protocol exists to serve
- [roadmap/](roadmap/README.md) — open proposals

## naming

cyber-seer was the name of the densification algorithm when it lived as a research page in [[cyber]]. seer is now the component; cyber-seer is its first method.

see [[tru]] for the measure · [[cybergraph]] for the substrate · [[cyb]] for the robot that carries it
