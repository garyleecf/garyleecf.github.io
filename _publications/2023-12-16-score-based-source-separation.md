---
title: 'Score-based source separation with applications to digital communication signals'
collection: publications
category: conference
permalink: /publication/2023-12-16-score-based-source-separation
excerpt: 'Introduces a score-based (generative) framework for separating superimposed sources, applying it to digital communication signals to improve interference rejection and separation fidelity over prior methods, with reproducible resources provided via a project page.'
date: 2023-12-16
venue: 'Advances in Neural Information Processing Systems'
citation: "T. Jayashankar, G. C. Lee, A. Lancho, A. Weiss, Y. Polyanskiy, and G. Wornell, “Score-based source separation with applications to digital communication signals,” Advances in Neural Information Processing Systems, vol. 36, pp. 5092–5125, 2023."
---

We propose a new method for separating superimposed sources using diffusion-based generative models. Our method relies only on separately trained statistical priors of independent sources to establish a new objective function guided by maximum a posteriori estimation with an α-posterior, across multiple levels of Gaussian smoothing. Motivated by applications in radio-frequency (RF) systems, we are interested in sources with underlying discrete nature and the recovery of encoded bits from a signal of interest, as measured by the bit error rate (BER). Experimental results with RF mixtures demonstrate that our method results in a BER reduction of 95\% over classical and existing learning-based methods. Our analysis demonstrates that our proposed method yields solutions that asymptotically approach the modes of an underlying discrete distribution. Furthermore, our method can be viewed as a multi-source extension to the recently proposed score distillation sampling scheme, shedding additional light on its use beyond conditional sampling. The project webpage is available at https://alpha-rgs.github.io.
