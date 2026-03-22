---
title: 'Exploiting Temporal Structures of Cyclostationary Signals for Data-Driven Single-Channel Source Separation'
collection: publications
category: conference
permalink: /publication/2022-11-17-cyclostationary-single-channel-separation
excerpt: 'Exploits cyclostationary temporal structure to enable data-driven single-channel source separation, improving separation quality while reducing computational burden compared with generic deep models by embedding signal-specific temporal cues.'
date: 2022-11-17
venue: '2022 IEEE 32nd International Workshop on Machine Learning for Signal Processing (MLSP)'
citation: "G. C. Lee, A. Weiss, A. Lancho, J. Tang, Y. Bu, Y. Polyanskiy, and G. W. Wornell, “Exploiting temporal structures of cyclostationary signals for data-driven single-channel source separation,” in 2022 IEEE 32nd International Workshop on Machine Learning for Signal Processing (MLSP). IEEE, 2022, pp. 1–6."
---

We study the problem of single-channel source separation (SCSS), and focus on cyclostationary signals, which are particularly suitable in a variety of application domains. Unlike classical SCSS approaches, we consider a setting where only examples of the sources are available rather than their models, inspiring a data-driven approach. For source models with underlying cyclostationary Gaussian constituents, we establish a lower bound on the attainable mean-square-error (MSE) for any separation method, model-based or data-driven. Our analysis further reveals the operation for optimal separation and the associated implementation challenges. As a computationally attractive alternative, we propose a deep learning approach using a U-Net architecture, which is competitive with the minimum MSE estimator. We demonstrate in simulation that, with suitable domain-informed architectural choices, our U-Net method can approach the optimal performance with substantially reduced computational burden.
