---
tags: cyber, cyb, seer, roadmap
crystal-type: process
crystal-domain: cyber
status: proposal
alias: learned proposal, gflownet focus flow, gflownet proposal, learned link proposal, GFlowNet, gflownet
---
# learned proposal

formal proposal. a learned proposer for [[seer]]: a Generative Flow Network that samples candidate [[cyberlinks]] in proportion to what they would settle for, using [densification](../specs/densification.md) as its analytical teacher.

## 0. the invariants this proposal must not break

- the proposer lives on the neuron's side, outside the [[focusing]] contraction. it never computes $\phi^*$ and never changes how tru does. tru stays bit-identical; learning happens here.
- the reward is the protocol's. the proposer samples in proportion to the neuron's expected settlement under [[rewards]] — the surprise-gated $\Delta\phi^+$, Shapley-divided — net of cost. nothing in this design introduces a second score for tru to honor.
- public aggregates only ([interface](../specs/interface.md), invariant 3).

## 1. the problem

a [[neuron]] choosing what to link faces a combinatorial search: which [[particles]] to connect, with what conviction, to get the most from a finite budget of will. the question is whether a learned model can propose high-value edits — a distribution over good edits, in proportion to their value, rather than the single best one.

## 2. why GFlowNets

a GFlowNet (Bengio et al. 2021) constructs structured objects by sequential actions and produces samples with probability proportional to a reward:

$$p_\theta(x) \propto R(x)$$

reinforcement learning finds the mode — the one best action — which for a knowledge graph means monoculture: every neuron proposes the same link. a GFlowNet samples the distribution, so proposals stay diverse in proportion to quality. MCMC also samples the distribution, but a GFlowNet is amortized: once trained, one sample is one forward pass, with no mixing time or burn-in. the training objective is trajectory balance (Malkin et al. 2022):

$$\log \frac{Z \prod_t p_F(s_{t+1} \mid s_t)}{\prod_t p_B(s_t \mid s_{t+1}) \, R(x)} = 0$$

with forward policy $p_F$, backward policy $p_B$, partition function $Z$; credit propagates over full trajectories via sub-trajectory balance.

## 3. the reward

the reward is what the neuron is paid, read from [[rewards]]:

$$R(x) = \exp\Big(\beta \big[\, \rho(x)\,\Delta\phi^+_\nu(x) \;-\; c(x) \;+\; u(x) \,\big]\Big)$$

- $\Delta\phi^+_\nu(x)$ — the neuron's standalone directed impulse for the edit, [[rewards]] §6 propose phase: exact, locality-bounded, in the fixed $T(\varepsilon)$ steps of [[arithmetic]]. this is the ceiling of what settles among substitutes.
- $\rho(x)$ — surprise, [[rewards]] §5: the BTS gate that pays nothing for a copy however large its impulse. this is the novelty term, and it is already the protocol's, not a design choice here.
- $c(x)$ — will and conviction the edit spends, plus storage if it creates a particle.
- $u(x)$ — the neuron's private utility (answer a query, complete a pattern). outside the protocol; the one term the neuron sets.

the exponential form is the optimal proposal distribution under a finite budget ([[universal law]]). densification's signals are not in $R$; they enter as the teacher (§4) and as priors that shape the search.

## 4. densification as teacher

[densification](../specs/densification.md) and the proposer solve the same problem by different means:

| | densification | learned proposal |
|---|---|---|
| approach | analytical: Fiedler vector, articulation points, focus hubs | learned: policy network, trajectory balance |
| signal | $\Delta\lambda_2$, resilience, $\Delta J$ | expected settlement |
| output | ranked top-$K$ | distribution over candidates |
| diversity | deterministic | stochastic, proportional to value |
| phases | explicit, from $\lambda_2$ | emergent from the cost term |
| cost | cheap | training plus inference |

they compose. densification's Fiedler-optimal links pre-train the proposer by behavioural cloning; the proposer then generalizes past the spectral signal — semantic shortcuts, multi-hop bridges, links that raise $\Delta\phi^+$ in ways the Fiedler vector does not predict. densification's three phases emerge in the learned policy on their own: early, when cost is low, structural links have the highest settlement-per-cost; late, the exponential cost crushes everything but high-impulse semantic links. the proposer is never told which phase it is in.

one caution from [[superadditivity]]: bridges raise $\lambda_2$ and lower syntropy, and the mint pays for directed syntropy. so a teacher that only knows bridges teaches links that settle for little. the cloning phase should use densification's semantic-phase proposals as much as its bridge-phase ones, and the settlement signal decides which lessons survive.

## 5. the loop

```
1. snapshot φ*, V_k, λ₂ from tru; the neuron's ego-net from the graph
2. the proposer samples a batch of candidate edits
   (add a cyberlink, raise conviction on an axon, attach evidence)
3. score each: Δφ⁺_ν(x) via the propose-phase marginal — or the surrogate (§6, Q1)
4. filter by will, guards; the neuron signs the subset it wants
5. tru measures the realized Δφ⁺ at settlement
6. train the proposer on realized settlement
7. repeat
```

## 6. open questions

### Q1 — a surrogate for the marginal

the exact per-candidate value is available: [[rewards]] §6 defines the neuron's standalone marginal as a locality-bounded recompute on its $O(\log 1/\varepsilon)$-hop neighbourhood in fixed steps, and [[impulse]] is the same quantity measured. what the exact recompute cannot do is score thousands of candidates per proposal step on a phone. the open question is a surrogate: a GNN trained on realized $\Delta\phi^+$ over local subgraphs, $O(1)$ per evaluation; or personalized push-back updates, $O(1/\varepsilon)$ per single-edge change; or a low-rank spectral update. the proposer is only as good as this surrogate — a poor one proposes noise. the exact marginal remains the scoring of record for whatever the neuron actually signs.

### Q2 — action spaces of $10^6$ and beyond

published GFlowNets construct graphs of tens of nodes with thousands of actions per step; the cybergraph has billions of particles. three reductions: hierarchical actions (namespace first, particle second, $O(\sqrt N)$ per level); focus-guided masking (only particles with $\phi^* > \varepsilon$ as targets — [[universal law]] says most focus sits on a small fraction); and per-neuron proposers over each neuron's own context, the global effect emerging from many local ones. the third matches the architecture. the org has an in-house GFlowNet trainer, built for compiler cost optimization in [[trisha]]; it is a starting point for the training loop, not for the action space.

### Q3 — privacy

training needs to see which edits improved $\phi^*$; individual cyberlinks are private. the resolution is invariant 3: the proposer reads public aggregates — $\phi^*$, axon weights, spectral positions — and the neuron's own ego-net, and the neuron decides privately what to sign. the proposer cannot optimize for another neuron's private pattern, which is the right restriction.

### Q4 — provability

a proposer that is a [[nox]] program produces a [[zheng]] trace: this policy, on this public state, produced these candidates. that proves the process, not the quality — quality comes from settlement. the harder question is whether training can be proved: gradient steps on the trajectory-balance loss as a nox program, giving verified model updates. open.

## 7. honest assessment

| aspect | status | confidence |
|---|---|---|
| GFlowNet theory | mature, peer-reviewed | high |
| GFlowNets for graph construction | demonstrated (DAG-GFlowNet) | high |
| at $10^6$+ actions | undemonstrated | low |
| surrogate for $\Delta\phi^+$ | research question | medium |
| privacy-compatible training | feasible on public aggregates | medium |
| provable proposals | architecturally possible | medium |
| provable training | open | low |
| the measure it needs | [[tru]] focusing, impulse, rewards — built | — |

the direction is valid and the architecture is compatible. what has changed since the first draft is the dependency: the measure this proposer learns from is built. what it still needs is the settlement loop running on a live graph, so realized $\Delta\phi^+$ exists to train on.

## 8. what to do first

1. the surrogate, as its own question — any proposer, learned or not, needs a fast estimate of the marginal; this is worth solving regardless of GFlowNets
2. a synthetic prototype — $10^4$ particles with known $\phi^*$; does the proposer learn to sample high-$\Delta\phi^+$ links, and how does diversity compare to random and greedy baselines?
3. integrate when settlement is live — train on realized values from a real graph, not on the surrogate

## references

1. E. Bengio et al., Flow Network based Generative Models for Non-Iterative Diverse Candidate Generation, NeurIPS 2021
2. N. Malkin et al., Trajectory Balance: Improved Credit Assignment in GFlowNets, NeurIPS 2022
3. T. Deleu et al., DAG-GFlowNet: Bayesian Structure Learning with GFlowNets, ICML 2022
4. N. Malkin et al., GFlowNets and Variational Inference, ICLR 2023
5. E. Bengio et al., GFlowNet Foundations, JMLR 2023

see [densification](../specs/densification.md) for the teacher · [[rewards]] for the reward · [[impulse]] for the measured quantity · [[collective focus theorem]] for why exponential proposals are optimal
