---
title: 'MARHO: Hybrid Task Offloading in Maritime MEC via Multi-Agent Reinforcement Learning'
collection: publications
category: manuscripts
permalink: /publication/2025-11-25-marho-maritime-marl
excerpt: 'Introduces MARHO, a multi-agent reinforcement learning approach for hybrid task offloading in maritime MEC architectures, coordinating agents to reduce average latency and improve service performance compared with existing benchmark strategies.'
date: 2025-11-25
venue: 'IEEE Open Journal of the Communications Society'
citation: "J. Ning, A. Li, G. C. Lee, S. Sun, and T. Yang, “MARHO: Hybrid task offloading in maritime mec via multi-agent reinforcement learning,” IEEE Open Journal of the Communications Society, vol. 6, pp. 10 322–10 337, 2025."
---

This paper presents MARHO, a Multi-Agent Reinforcement learning-based Hybrid task Offloading framework, designed for maritime mobile edge computing (MEC) environments characterized by time-varying wireless channels, heterogeneous workloads, and stringent quality of service (QoS) requirements. The considered MEC architecture integrates uncrewed surface vessels (USVs), uncrewed aerial vehicles (UAVs), and a ship platform with high-performance edge servers. USVs generate sensing and computing tasks that can be (i) executed locally, (ii) offloaded to UAVs for aerial edge processing, or (iii) relayed through UAVs to the ship under line-of-sight (LoS) links. The system model jointly captures queueing dynamics, wireless transmission latency, computation delay, and battery constraints. The hybrid offloading problem is formulated as a Decentralized Partially Observable Markov Decision Process (Dec-POMDP), where each USV acts as an agent that decides its offloading mode under partial observations. To solve this, MARHO employs a centralized training and decentralized execution (CTDE) scheme, enabling agents to learn resource-aware strategies that effectively balance communication and computation. A Gym-based simulation environment is developed, integrating realistic maritime signal propagation, queue dynamics, and mixed offloading scenarios. The experimental results under different task loads demonstrate that MARHO consistently achieves higher throughput and has a lower average latency compared to the existing benchmark.
