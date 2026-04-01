---
layout: single
title: "What is the deal with 5G? Is it really faster?"
date: 2026-04-01
categories:
  - 5G
  - 6G
tags:
  - 5G
  - 6G
  - eMBB
  - URLLC
  - mMTC
excerpt: "Most people think 5G means faster downloads. It does---but is that all? The deeper story is about what 'faster' even means, and why three different answers lead to three different engineering problems."
author_profile: true
---

When I tell people I work on 5G---and 6G, but more on that in future posts---a version of the same comment comes up. "My 4G LTE is perfectly fine for streaming and browsing. Do I actually need to upgrade to 5G?" Which is a fair comment. This leads to the natural question: if 4G is fast enough, what is the whole deal with 5G? What problem does it actually solve?

The complicated answer is that 5G is very different in terms of how cellular networks operate behind the scenes, which is generally not visible to the everyday user. But rather than getting into that, this post focuses on what 5G was meant to be for. Because it was not designed to simply make downloads faster or streaming smoother. It could, with the extra bandwidth, but that is not the revolution. Rather, 5G was designed with enterprise in mind (think smart factories, hospitals, autonomous vehicles). To see why, we need to revisit what "fast" actually means.

## Rate is a fraction. There is more than one way to make it bigger.

When we talk about data rate or communication rate, we mean the amount of data divided by time---i.e., bits per second. If we want a higher rate, the obvious move is to send more data per transmission. But another way is actually to shrink the denominator, and finish the transmission in less time.

Most of us picture the first case. When downloading a large file, the data size is fixed, and we want the transfer to finish quickly. We do this by "expanding" our pipe, using more resources and packing more bits per symbol. This is **eMBB: Enhanced Mobile Broadband**, the flavor of "fast" that consumers recognize. 

But are there alternative perspectives to this?

## What if the data is tiny, but the time has to be near-zero?

Imagine a robot on a factory floor receiving time-sensitive commands from a controller. Each command is maybe a few tens to hundred bytes, messages that are not very big. But the robot cannot afford to wait! A delay of more than a millisecond could mean a missed step, a damaged part, or worse, an accident or injury. Here, the "data" in the numerator is small; yet, what matters most is that the denominator, i.e., time or latency, is kept extremely low. (And also that the link almost never fails.)

This is **URLLC: Ultra-Reliable Low-Latency Communication**. The target is generally end-to-end latency on the order of sub-millisecond with reliability of 99.999% (we sometimes call it "five nines"). One can imagine this being highly relevant and important for remote teleoperated surgery, autonomous vehicles reacting to hazards, or electrical grid control.

These requirements are hard, not because the data is large, but because of the physics of wireless communication (fading, interference, retransmissions) fights against guaranteed low latency. The required setup looks almost nothing like eMBB. We now have a completely different set of tradeoffs, as well as a new set of tools and techniques to realize these, such as short packets, grant-free access, dedicated resource scheduling and spatial diversity. 

## What if you have a million devices, each barely transmitting at all?

Now imagine a city where every electricity meter, water pipe sensor, parking space, and shipping container is wirelessly connected. Each device sends a small report every few minutes. Individually, the data rate per device is negligible. But you might have tens of thousands, or even millions of these devices packed in a small area, all sharing the same network.

This is **mMTC: massive Machine-Type Communication**, which is effectively when we scale IoT use case significantly. The challenge is no longer throughput or latency, but rather *connection density* and *energy efficiency*. These devices often run on small batteries and need to last years in the field. And while the aggregate data across all these devices does add up to significant throughput, the bigger challenge is that every device brings its own identity---and with it, authentication headers, addressing, protocol handshakes. This overhead per message is no longer negligible when you multiply it by a million. The protocols designed for cellular phones (to negotiate a connection, exchange credentials, then transmit) were not meant for the deployment density of million devices waking up sporadically in a single cell. Such a network has to handle extreme congestion without demanding much from each device node.

So the same question of "how do we get a higher rate from the network?" gives rise to three completely different considerations, depending on which part of the fraction you are squeezing, and for whom.

## 5G was designed to handle all three

5G (IMT-2020, standardized from around 2018) was explicitly built around these different perspectives, giving rise to a single flexible network (the so-called "5G New Radio (NR)") configurable for eMBB, URLLC, or mMTC depending on the deployment. However, in practice, most consumer 5G today is eMBB, for faster downloads in dense urban areas and better coverage in stadiums (e.g., the ``Taylor Swift Concert Effect'' on mobile networks [link](https://about.rogers.com/news-ideas/taylor-swift-fans-set-new-record-for-mobile-data-use-at-rogers-centre/) ). URLLC and mMTC capabilities are the part of 5G that industry is still building out, mostly in private 5G deployments at factories and ports/logistics hubs. That is where the more interesting engineering continues to happen.

## 6G expands the envelope further
And so, what is 6G? Here's a quick look in a nutshell.

Fast forward to 2023, ITU released the IMT-2030 framework (the *de facto* vision for 6G). The familiar triangle that describes 5G's 3 use cases sits in the middle. But moving forward, they have evolved with ambitious targets. Immersive Communication (from eMBB) targets for peak data rates up to 1 Tbps, Hyper-Reliable Low Latency Communication (from URLLC) strives to achieve 0.1 ms latency with "seven-nines" reliability, and Massive Communication (from mMTC) caters to connection densities an order of magnitude higher. 

<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/imt2030-official.png" alt="ITU-R IMT-2030 framework diagram showing the six usage scenarios for 6G" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">The six usage scenarios defined in the ITU-R IMT-2030 framework. Three evolve from 5G's service classes; three are additions that define what makes 6G genuinely new.</figcaption>
</figure>

But the more interesting part of IMT-2030 is not the bigger numbers or more ambitious targets; rather, it is how three additional scenarios have been identified that have no counterpart in 5G, further "expanding" the triangle into a hexagon. They are, namely, 

**Integrated Sensing and Communication (ISAC)**: the network no longer just carry data; rather, it can also use the same hardware and its own radio signals to sense the physical environment, detecting objects and estimating device locations. The antenna that used to only convey information is now also a radar.

**AI and Communication**: rather than running AI on top of the network as an afterthought, intelligence ought to be designed into the network architecture itself; for example, they can be used to revolutionize the way we do channel estimation, resource allocation, beam management, and network resource optimization. The network becomes an intelligent and proactive agent, not just a passive pipe.

**Ubiquitous Connectivity**: seamless integration of terrestrial cells with satellites and aerial platforms, so that coverage is no longer bounded by where a cell tower was economical to build. We can thus reach deep rural areas, and serve maritime and aviation industries, thereby realizing the goal of "connecting the unconnected".

Taken together, the vision for 6G is a shift from a communication network to a platform for communication, sensing, and computation---one that increasingly serves machines, infrastructure, and industrial systems as much as people holding phones.

## The bottom line

If your 4G works fine for streaming and browsing, that will probably continue to be the case. What 5G and 6G are trying to solve is the set of problems that comes next: connecting the physical world at scale, enabling latency-sensitive control over wireless links, and building a network infrastructure that industry can rely on.

All in all, "faster internet" can mean more than just faster download speeds. The more precise framing is: *higher rates for different kinds of traffic, with different reliability and latency requirements, for many more types of users than just humans with smartphones.* That distinction is also what drives some of the exciting research and development works in the space of 5G, 6G and beyond.

---

*Next in the series: we will spend some time to discuss more on the three new scenarios set forth in IMT-2030/6G, and what they might actually involve technically, together with where the active research efforts are.*
