---
tags: cyber, cyb, seer, spec
crystal-type: spec
crystal-domain: cyber
status: draft
alias: seer interface, proposal interface, seer contract
---
# interface

the contract between [[seer]], [[tru]], the [[cybergraph]], and the [[neuron]] that signs. seer is a pure function from public state to a ranked set of candidate signals, plus whatever private state a learned method keeps for itself.

## inputs

everything seer reads is public, per-epoch, and already computed by someone else.

| input | from | what it is |
|---|---|---|
| $\phi^*$, cyberank | [[focusing]] | the collective focus distribution and its per-particle reading |
| spectral positions $V_k$ | [[focusing]] | the bottom-$k$ Laplacian eigenvectors, Fiedler vector $v_2$ first; row $i$ is particle $i$'s coordinate |
| $\lambda_2$, $\kappa$ | [[focusing]] | algebraic connectivity and the contraction, per epoch |
| syntropy $J$ | [[focusing]] | how concentrated $\phi^*$ is |
| $\Delta\phi^+_\nu(S)$ | [[rewards]] §6, propose phase | the neuron's standalone directed impulse for a candidate set $S$ — the exact locality-bounded recompute on the neuron's $O(\log 1/\varepsilon)$-hop neighbourhood, in the fixed $T(\varepsilon)$ steps of [[arithmetic]] |
| signals, cyberlinks, particles | [[cybergraph]] | the graph itself, and the neuron's own ego-net |
| will, conviction | the neuron ([[cyb]]) | what the neuron can spend, and where it already stands |

seer reads the Fiedler vector; it does not run an eigensolver. tru emits $V_k$ every epoch, and the phase logic of [densification](densification.md) needs $v_2$ at tru's cadence, not faster.

## output

a proposal: a ranked or sampled set of candidate [[cyberlinks]] $(p, q, \tau, a, v)$ for one neuron, each carrying

- the predicted settlement $\hat{v}$ — what the neuron expects to be paid under [[rewards]] if this link enters the graph
- the structural score — $\Delta\lambda_2$, articulation bypass, or focus redistribution, per the method's phase
- the cost — will and conviction the link would spend
- the method and its confidence

the neuron decides. seer proposes, the owner signs (through [[cyb/parts/ward|ward]] and the vault in cyb, or the agent's own key), the [[signal]] goes out, tru measures the realized $\Delta\phi^+$ at settlement. that realized value is the training signal for any learned method.

## invariants

1. outside the contraction. seer never computes $\phi^*$, never participates in [[focusing]], never proposes a change to the iteration. tru's determinism is what [[zheng]] proves; nothing here may depend on it being otherwise.
2. settlement is the objective. a method ranks or samples by expected settlement under [[rewards]] — the surprise-gated $\Delta\phi^+$, Shapley-divided — net of cost. structural signals are priors that shape the search; they are never the quantity optimized. the protocol pays for directed syntropy that is valid and surprising; a copy of an obvious link scores zero however large its $\Delta\lambda_2$.
3. public aggregates only. individual cyberlinks are private to their neurons; $\phi^*$, axon weights, spectral positions are public. seer reads the public side and the neuron's own ego-net, never another neuron's. a learned method therefore optimizes publicly visible focus flow, which is the right objective.
4. proposal, then commitment. a method may be cheap and wrong; the neuron pays only when it signs. seer's output is advice with a predicted value attached; the prediction is scored against the realized settlement, and a method that mispredicts loses the neuron's trust before it loses the neuron's stake.
5. provable when it matters. a proposal produced by a [[nox]] program carries a [[zheng]] trace: this policy, run on this public state, produced these candidates. that proves the process, not the quality. quality comes from settlement.

## the structural–economic tension

densification's early phases raise $\lambda_2$ — bridges and bypasses that spread focus across the graph. [[superadditivity]] measured that connectivity raises the collective's advantage $\sigma$ and lowers syntropy $J$; the mint pays for directed syntropy. so a pure bridge can be exactly what the network needs and settle for little. the protocol's subsidy stream ([[rewards]] §the three streams) is where structural work is paid, if it is paid; how much, and by what rule, is open. seer reports both numbers — structural score and predicted settlement — and never pretends the first is the second.

see [densification](densification.md) for the first method · [[rewards]] for what settles · [[impulse]] for the quantity measured
