---
title: 'From Freshness to Effectiveness: Goal-Oriented Sampling for Remote Decision Making'
collection: publications
category: manuscripts
permalink: /publication/2026-02-11-goal-oriented-sampling-remote-decision
excerpt: 'Shows why freshness (AoI) alone can misalign with decision quality and proposes goal-oriented sampling strategies that prioritize effective information for remote decision-making, supported by analysis and simulations demonstrating improved outcomes.'
date: 2026-02-11
venue: 'IEEE Transactions on Information Theory'
citation: "A. Li, S. Wu, G. C. Lee, and S. Sun, “From freshness to effectiveness: Goal-oriented sampling for remote decision making,” IEEE Transactions on Information Theory, 2026"
---

\[[arXiv](https://arxiv.org/abs/2504.19507)\]

![](https://arxiv.org/html/2504.19507v3/x1.png)

Data freshness, measured by Age of Information (AoI), is highly relevant in networked applications such as Vehicle to Everything (V2X), smart health systems, and Industrial Internet of Things (IIoT). However, freshness alone does not always equate to utility in decision-making. In decision-critical settings, some stale data may be more valuable than fresh updates. Motivated by this, we move beyond AoI-centric policies and investigate how data staleness affects remote decision-making effectiveness under random delay and limited communication resources. To this end, we propose AR-MDP, an Age-aware Remote Markov Decision Process framework, which co-designs optimal sampling and remote decision-making under a sampling frequency constraint and random delay. To efficiently solve this problem, we design a new two-stage hierarchical algorithm, namely Quick Bellman-Linear-Program (QUICKBLP), where the first stage involves solving the Dinkelbach root of a Bellman variant and the second stage involves solving a streamlined linear program (LP). For the tricky first stage, we propose a new One-layer Primal-Dinkelbach Synchronous Iteration (ONEPDSI) method, which overcomes the re-convergence and non-expansive divergence present in existing per-sample multi-layer algorithms. Through rigorous convergence analysis of our proposed algorithms, we establish that the worst-case optimality gap in ONEPDSI exhibits exponential decay with respect to iteration K at a rate of O( 1/RK ). Through sensitivity analysis, we derive a threshold for the sampling frequency, beyond which additional sampling does not yield further gains in decision-making. Simulation results validate our analyses.
