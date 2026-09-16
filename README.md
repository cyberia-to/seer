---
title: seer
tags: cyber, cyb, seer, core, warriors
crystal-type: entity
crystal-domain: cyber
icon: "🔮"
alias: seer, cyber-seer, cyber/seer, link miner, mint miner, structure miner
---
# seer

a [[neuron]] holds a budget of will and a graph of [[particles]] it did not create. somewhere among the $O(N^2)$ pairs of particles that already exist is the [[cyberlink]] that would teach the graph the most — shift collective [[focus]] $\phi^*$ the furthest — for the will it costs. finding that pair is a search over public state, and [[tru]] prices every candidate exactly before a single token is spent: $\rho \cdot \Delta\phi^+$, surprise times proven impulse, net of cost ([[rewards]] §6). seer is the agent that runs the search and hands the winning candidates to the neuron to sign.

that is what a miner is: an agent that searches a space against a public, exactly-priced function and is paid for what it proves. seer's hash function is $\phi^*$; its hashrate is proven $\Delta\phi^+$ per epoch; its difficulty is the surprise gate $\rho$ times the exponential cost of links ([[universal law]]); its pool is the graph itself — evidence, not documentation; its duty cycle is the will it may spend. the two doctrines of [[warriors]] apply unchanged — make the machine earn, and report the true rate — the machine here is a neuron's will instead of a chip.

seer mines the mint. on $CYB a neuron is paid four ways ([[rewards]]):

- the mint — Shapley's share of the proven focus shift $\Delta\phi^+$ its links caused
- the subsidy — proof-of-work for settling other neurons' shares
- query fees
- stake

a different miner grinds nonces for the subsidy. seer grinds the pair space for the mint. two miners, two streams, same graph.

## why any chain

the price seer mines against is not specific to $CYB. it is defined by [[tru]]'s measure alone — any book whose settlement pays for proven focus shift can be mined the same way. and there is no single such book: [[cyber/research/oikos|oikos]] gives every token its own home book, one token one chain, and any [[neuron]] with a token can root one. $CYB is the reference implementation, not the only chain. the chain seer mines is whichever one the neuron is signing into; other books define their own streams past the mint, and seer mines whichever of them pays for focus.

## why it never creates a particle

the price above only exists for pairs of particles that already exist. a new particle's value is the entropy of content nobody has written yet — it exists once the particle is made, not before, so nothing prices it in advance the way $\rho \cdot \Delta\phi^+$ prices an edge. that is not a policy choice, it is the boundary of what a search over public state can do: mining is exact because the space is bounded and every answer is priceable in advance; creation is synthesis in an unbounded space, and its risks — hallucination, redundancy, storage paid before worth is known — are exactly the risks of an unpriceable search. seer stays on the priceable side. humans, models, and agents create particles; seer wires what they make into the graph it did not write. see [docs/link-production.md](docs/link-production.md) for the full boundary.

## when it stops

the stop is the same price, run to its conclusion. a pair is worth mining iff $\rho \cdot \Delta\phi^+$ exceeds its cost, and a graph where no remaining pair clears that bar is one where nothing about its structure would surprise the crowd — mined out, for now, for that neuron. no threshold to tune: the reward decides, from public state and the neuron's own ego-net.

three things follow from that, and two things do not follow yet:

- structural work runs out first. bridges and bypasses raise $\lambda_2$ and spread focus; the mint pays for concentration. [densification](specs/densification.md)'s phases end in maintenance, and bostrom's measured $\lambda_2 \approx 0.13$ means it had already ended there — only focus-redistributing links kept clearing the bar.
- mining never stops globally. every new particle arrives unwired, and wiring it in is existing→existing work again; [[temporal decay]] removes links and reopens pairs. mining is the digestion of creation, mined-out only per region and per epoch.
- a mined-out region is, by construction, one a learned policy trained on realized settlement will learn to leave alone on its own.

open:

1. the mint's stop is not proven to be the network's need. [[superadditivity]] measured that connectivity raises the collective's advantage $\sigma$ while it lowers syntropy $J$; the mint pays in the $J$ direction, and the subsidy is stake-blind proof-of-work, not a fund for structure. a graph can be mined out by the mint's own criterion while still under-connected for [[foculus]] finality. either concentrating links are what actually matters and the network is fine, or a structural term is missing from [[rewards]] — a question for that spec, and seer reports both numbers, structural score and predicted settlement, so the question can be settled from evidence rather than argued.
2. the loop's fixed point is not proven. tru's contraction guarantees $\phi^*$ converges each epoch on a fixed graph; miners changing the graph in response to $\phi^*$, epoch over epoch, is a different dynamical system, and whether it settles or oscillates is open (see [docs/link-production.md](docs/link-production.md), question 4).

## invariants

1. outside the contraction — seer never computes $\phi^*$ and never touches [[focusing]]. learning lives here so that tru stays bit-identical on every machine.
2. the mint is the objective — seer ranks or samples by expected settlement net of cost. structural signals are priors that shape the search, never the quantity optimized.
3. no new particles — seer proposes edges between particles that exist.
4. honesty as a feature — every proposal carries a predicted settlement, and every settled epoch scores that prediction against what tru measured. a policy that mispredicts loses the neuron's trust before it loses the neuron's stake.

## methods

| method | kind | signal | status |
|---|---|---|---|
| [densification](specs/densification.md) | analytical | Fiedler vector → $\Delta\lambda_2$ per link; three phases, bridge → mesh → semantic | specified, unbuilt |
| [learned policy](roadmap/learned-policy.md) | learned | a GFlowNet that samples links in proportion to expected settlement, densification as teacher | proposal |

## map

- [specs/interface.md](specs/interface.md) — the contract: inputs from tru and the graph, the mining loop, what seer emits, the invariants
- [specs/densification.md](specs/densification.md) — cyber-seer, the analytical method
- [docs/link-production.md](docs/link-production.md) — why: the intelligence problem, and where mining ends and creation begins
- [roadmap/](roadmap/README.md) — open proposals

## naming

cyber-seer was the densification algorithm when it lived as a research page in [[cyber]]. seer is the component; cyber-seer is its first method.

see [[tru]] for the measure · [[rewards]] for the streams · [[warriors]] for the doctrine · [[cyb]] for the body that runs it
