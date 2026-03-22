---
title: 'Lyapunov-guided Deep Reinforcement Learning for Semantic-aware AoI Minimization in UAV-assisted Wireless Networks'
collection: publications
category: manuscripts
permalink: /publication/2025-03-27-lyapunov-guided-drl-semantic-uav
excerpt: 'Combines Lyapunov optimization with deep reinforcement learning to control semantic extraction and transmission in UAV-assisted networks, minimizing semantic-aware AoI and improving information recovery quality and timeliness relative to existing approaches.'
date: 2025-03-27
venue: 'IEEE Transactions on Wireless Communications'
citation: "Y. Long, S. Gong, S. Sun, G. C. Lee, L. Li, and D. Niyato, “Lyapunov-guided deep reinforcement learning for semantic-aware AOI minimization in UAV-assisted wireless networks,” IEEE Transactions on Wireless Communications, 2025."
---

\[[arXiv](https://arxiv.org/abs/2409.13580)\]

![](https://arxiv.org/html/2409.13580v1/x1.png)

This paper investigates an unmanned aerial vehicle (UAV) assisted semantic network where the ground users (GUs) periodically capture and upload the sensing information to a base station (BS) via UAVs’ relaying. Both the GUs and the UAVs can extract semantic information from large-size raw data and transmit it to the BS for recovery. Smaller-size semantic information reduces latency and improves information freshness, while larger-size semantic information enables more accurate data reconstruction at the BS, preserving the value of original information. We introduce a novel semantic-aware age-of-information (SAoI) metric to capture both information freshness and semantic importance, and then formulate a time-averaged SAoI minimization problem by jointly optimizing the UAV-GU association, the semantic extraction, and the UAVs’ trajectories. We decouple the original problem into a series of subproblems via the Lyapunov framework and then use hierarchical deep reinforcement learning (DRL) to solve each subproblem. Specifically, the UAV-GU association is determined by DRL, followed by the optimization module updating the semantic extraction strategy and UAVs’ deployment. Simulation results show that the hierarchical structure improves learning efficiency. Moreover, it achieves low AoI through semantic extraction while ensuring minimal loss of original information, outperforming the existing baselines.
