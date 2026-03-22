---
layout: single
title: "Your 4G Works Fine. So What Is 5G Actually For?"
date: 2026-03-22
categories:
  - 5G
  - 6G
tags:
  - 5G
  - 6G
  - eMBB
  - URLLC
  - mMTC
  - explainer
excerpt: "Most people think 5G means faster downloads. It does — but that's the least interesting part. The deeper story is about what 'faster' even means, and why three very different answers lead to three very different engineering problems."
author_profile: true
---

If you have 4G LTE and a decent Wi-Fi router at home, your internet probably feels fine. Videos load instantly, calls are clear, pages snap open. So when someone says 5G is revolutionary, or that 6G is already being designed, a reasonable response is: *why?* What problem is actually being solved here?

The short answer is that 5G is not primarily about making your YouTube smoother. It is about expanding what wireless networks can do *at all* — into factories, hospitals, autonomous vehicles, and infrastructure. To see why, it helps to think carefully about what "faster" actually means.

## Rate is a fraction. There is more than one way to make it bigger.

At the most basic level, a communication rate is data divided by time. Bits per second. If you want a higher rate, you can increase the numerator — send more data per transmission — or decrease the denominator — finish transmitting in less time.

Most of us, when we think about fast internet, are picturing the first case. Downloading a large file: the data size is fixed (say, a 4K movie at 10 GB), and we want the transfer to finish quickly. The solution is straightforward in principle — widen the channel, use more of the spectrum, pack more bits into each transmission. This is **eMBB: Enhanced Mobile Broadband**. It is the flavour of "fast" that most consumers are familiar with, and it is what 4G was optimised for.

But watch what happens when you tilt the fraction differently.

## What if the data is tiny, but the time has to be near-zero?

Imagine a robot arm on a factory floor receiving motion commands from a controller. Each command is maybe a few hundred bytes. Not a large file. But the arm cannot afford to wait — a delay of more than a millisecond could mean a missed step, a damaged part, or an injury. The "data" in the numerator is small. What matters is that the denominator — latency — is kept extremely low, and that the link almost never fails.

This is **URLLC: Ultra-Reliable Low-Latency Communication**. The target is end-to-end latency on the order of one millisecond with reliability of 99.9999% — sometimes called "five nines" or "six nines." Think remote surgery, autonomous vehicles reacting to hazards, electrical grid control, or haptic feedback over a network (the so-called tactile internet).

These requirements are not hard because the data is large. They are hard because the physics of wireless communication — fading, interference, retransmissions — fights against guaranteed low latency. The engineering solutions look almost nothing like eMBB. Short packets, grant-free access, dedicated resource scheduling, spatial diversity. A completely different set of tradeoffs.

## What if you have a million devices, each barely transmitting at all?

Now imagine a city where every electricity meter, water pipe sensor, parking space, shipping pallet, and agricultural field monitor is wirelessly connected. Each device sends a small report every few minutes. Individually, the data rate per device is negligible. But you might have tens of thousands of these devices per square kilometre, all sharing the same network.

This is **mMTC: massive Machine-Type Communication** — the IoT use case taken seriously. The challenge is no longer latency or peak throughput. It is *connection density* and *energy efficiency*. These devices often run on small batteries and need to last years in the field. They need to connect reliably even when the network is extremely congested. And the protocols that work fine for smartphones — which negotiate a connection, exchange authentication messages, then transmit — are far too heavyweight when you have a million devices waking up sporadically.

So the same question — how do we get a higher rate from the network? — produces three completely different engineering disciplines depending on which part of the fraction you are squeezing, and for whom.

## 5G was designed to handle all three

The first generation explicitly built around this three-way split is 5G (IMT-2020, standardised from around 2018). The idea was a single flexible air interface — New Radio — that could be configured for eMBB, URLLC, or mMTC depending on the deployment. Millimetre-wave frequencies for extreme eMBB throughput. Dedicated numerologies and scheduling for URLLC. Lean protocols and power-saving modes for mMTC.

In practice, most consumer 5G today is eMBB — faster downloads in dense urban areas, better coverage in stadiums. The URLLC and mMTC capabilities are the part of 5G that industry is still building out, in private 5G deployments at factories, ports, and logistics hubs. That is where the more interesting engineering is happening.

## 6G expands the envelope further

The ITU released the IMT-2030 framework — the official vision for 6G — in 2023. On the familiar axes, the numbers are ambitious: peak data rates up to 1 Tbps (versus 20 Gbps for 5G), air-interface latency targets of 0.1 ms, and connection densities an order of magnitude higher.

But the more interesting part of IMT-2030 is not the bigger numbers. It is the three entirely new usage scenarios that have no direct equivalent in 5G.

<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/imt2030-official.png" alt="ITU-R IMT-2030 framework diagram showing the six usage scenarios for 6G" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">The six usage scenarios defined in the ITU-R IMT-2030 framework. Three evolve from 5G's service classes; three are additions that define what makes 6G genuinely new.</figcaption>
</figure>

The three evolved scenarios — Immersive Communication, Hyper-Reliable Low Latency, and Massive Communication — are essentially eMBB, URLLC, and mMTC with sharper targets. Faster, more reliable, denser. The three new scenarios are where IMT-2030 departs from its predecessor.

**Integrated Sensing and Communication (ISAC)**: the network does not just carry data — it uses its own radio signals to sense the physical environment, detecting objects, estimating positions, and building maps of the surroundings. The antenna that was only a transmitter is now also a radar.

**AI and Communication**: rather than running AI on top of the network as an afterthought, intelligence is designed into the network architecture itself — for channel estimation, resource allocation, beam management, and self-optimisation. The network becomes an active learner, not just a passive pipe.

**Ubiquitous Connectivity**: seamless integration of terrestrial cells with satellites and high-altitude platforms, so that coverage is no longer bounded by where a cell tower was economical to build. Deep rural, maritime, aviation — all first-class citizens.

Taken together, the vision for 6G is a shift from a communication network to a platform for communication, sensing, and computation — one that increasingly serves machines, infrastructure, and industrial systems as much as people holding phones.

## The bottom line

If your 4G works fine for streaming and browsing, that will probably remain true. Consumer broadband is a solved problem at the scale of an individual user. What 5G and 6G are trying to solve is the set of problems that come next: connecting the physical world at scale, enabling latency-sensitive control over wireless links, and building a network infrastructure that industry can rely on the way it currently relies on wired ethernet.

"Faster internet" is a shorthand. The more precise framing is: *higher rates for different kinds of traffic, with different reliability and latency requirements, for many more types of users than just humans with smartphones.*

That distinction is where almost all of the interesting engineering lives.

---

*Next in the series: **What Makes 6G Different** — a closer look at the three new IMT-2030 scenarios (ISAC, native AI, and ubiquitous connectivity), what each one actually involves technically, and where the active research is.*
