---
title: 'On Neural Architectures for Deep Learning-Based Source Separation of Co-Channel OFDM Signals'
collection: publications
category: conference
permalink: /publication/2023-05-05-neural-architecture-ofdm-separation
excerpt: 'Evaluates and refines neural architectures for separating co-channel OFDM signals from a single channel, identifying design choices that markedly improve separation and reporting architectures that deliver roughly 30 dB performance gains in studied settings.'
date: 2023-05-05
venue: 'ICASSP 2023-2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)'
citation: "G. C. Lee, A. Weiss, A. Lancho, Y. Polyanskiy, and G. W. Wornell, “On neural architectures for deep learning-based source separation of co-channel OFDM signals,” in ICASSP 2023-2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP). IEEE, 2023, pp. 1–5."
---

We study the single-channel source separation problem involving orthogonal frequency-division multiplexing (OFDM) signals, which are ubiquitous in many modern-day digital communication systems. Related efforts have been pursued in monaural source separation, where state-of-the-art neural architectures have been adopted to train an end-to-end separator for audio signals (as 1-dimensional time series). In this work, through a prototype problem based on the OFDM source model, we assess—and question—the efficacy of using audio-oriented neural architectures in separating signals based on features pertinent to communication waveforms. Perhaps surprisingly, we demonstrate that in some configurations, where perfect separation is theoretically attainable, these audio-oriented neural architectures perform poorly in separating co-channel OFDM waveforms. Yet, we propose critical domain-informed modifications to the network parameterization, based on insights from OFDM structures, that can confer about 30 dB improvement in performance.
