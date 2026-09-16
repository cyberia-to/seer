---
title: seer
tags: cyber, cyb, seer, core, warriors
crystal-type: entity
crystal-domain: cyber
icon: "🔮"
alias: seer, cyber-seer, cyber/seer, link miner, mint miner, structure miner
---
# seer

seer is a miner. its chain is [[cyber]]. it mines the mint.

a [[neuron]] is paid four ways ([[rewards]]): the mint — Shapley's share of the proven focus shift $\Delta\phi^+$ its links caused; the subsidy — proof-of-work for settling other neurons' shares; query fees; and stake. seer is the agent that earns the first. it reads the graph and the measure, finds the [[cyberlinks]] that would shift [[focus]] the most per unit of will, and hands them to the neuron to sign. the settlement miner grinds nonces for the subsidy; seer grinds the link space for the mint. two miners, two streams.

its hash function is $\phi^*$. its hashrate is proven $\Delta\phi^+$ per epoch. its difficulty is the surprise gate $\rho$ times the exponential cost of links. its pool is the graph itself — evidence, not documentation. its duty cycle is the will it is allowed to spend. the two doctrines of [[warriors]] — make the machine earn, and report truthfully — apply without change; the machine here is a neuron's will instead of a chip.

## the one limitation

seer never creates a particle. it optimizes the structure of the graph as it stands: which existing [[particles]] should be connected, with what conviction. creating a particle is a different task by nature — synthesis in an unbounded space, whose value is the entropy of new content and whose risks are hallucination, redundancy, and storage paid before worth is known. mining is search in a bounded space, $O(N^2)$ pairs, where the exact value of every candidate is computable from public state before a single token is spent ([[rewards]] §6). a miner needs no understanding of content to be perfect at this; seer is content-blind by construction. humans, models, and agents create; seer wires what they make into the graph. see [docs/link-production.md](docs/link-production.md) for the boundary between the two.

## when mining stops

a graph that does not need optimization is one where nothing about its structure would surprise the crowd. that is not a slogan; it is the reward. the mint pays directed syntropy gated by surprise: a link the crowd already expects settles for nothing however large its $\Delta\phi^+$, and a link that adds no directed syntropy settles for nothing however surprising. so a candidate is worth mining iff its expected settlement exceeds the will it costs, and when no pair in a neuron's reach clears that bar, seer idles. the stop is built into the reward — no threshold to tune, decidable per neuron from public state and its own ego-net.

three consequences, and two open questions:

- structural work stops first. bridges and bypasses raise $\lambda_2$ and spread focus; the mint pays for concentration. [densification](specs/densification.md)'s phases end in maintenance, and on bostrom they had already ended ($\lambda_2 \approx 0.13$). past that point only focus-redistributing links — hubs to undervalued particles — clear the bar.
- mining never stops globally. every created particle arrives unwired, and wiring it in is existing→existing work. [[temporal decay]] removes links and reopens pairs. mining is the digestion of creation: the mined-out state is per region and per epoch, and it lasts until something new arrives.
- copies are the floor. a region is mined out when every remaining link is predictable. this is why a learned policy trained on realized settlement learns to stop on its own.

open:

1. the mint's stop is not the network's need. [[superadditivity]] measured that connectivity raises the collective's advantage $\sigma$ and lowers syntropy $J$; the mint pays in the $J$ direction, and the subsidy is stake-blind proof-of-work, not a fund for structure. a graph can be mined out by the mint's criterion while still under-connected for [[foculus]] finality. either focus-concentrating links are the ones that matter and the network is fine, or a structural term is missing from the reward. that is a question for [[rewards]], and seer reports both numbers — structural score and predicted settlement — so it can be answered from evidence.
2. the loop has no proven fixed point. tru's contraction guarantees $\phi^*$ converges each epoch on a fixed graph; miners changing the graph in response to $\phi^*$ is a different dynamical system. whether it settles or oscillates is open ([docs/link-production.md](docs/link-production.md), question 4).

## invariants

1. outside the contraction. seer never computes $\phi^*$ and never touches [[focusing]]. learning lives here, so tru stays bit-identical on every machine.
2. the mint is the objective. seer ranks or samples by expected settlement under [[rewards]] net of cost. structural signals are priors that shape the search, never the quantity optimized.
3. no new particles. seer proposes edges between particles that exist.
4. honesty as a feature. every proposal carries a predicted settlement; every settled epoch scores the prediction against what tru measured. a policy that mispredicts loses the neuron's trust before it loses the neuron's stake.

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
