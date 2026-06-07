---
layout: single
title: "Can a 6G Base Station Double as a Radar?"
date: 2026-06-05
categories:
  - 6G
tags:
  - ISAC
  - Sensing
  - Radar
  - 6G
  - AI-Native
excerpt: "A 6G base station and a radar have more in common than it might seem. ISAC---Integrated Sensing and Communication---is the 6G scenario that takes that similarity seriously. Here is where the value proposition holds up, and where it deserves a harder look."
author_profile: true
---

This is the second post in a three-part series on 6G's new scenarios. The [first post]({% post_url 2026-04-08-uncovering-hidden-structures-in-wireless-systems-with-ai %}) covered *AI and Communication*. This one is about **Integrated Sensing and Communication (ISAC)**. The third will cover Ubiquitous Connectivity (focusing on Non-Terrestrial Networks).

---

A radar and a base station look different from the outside. One is pointed at a certain region of interest (e.g., the sky scanning for aircraft or the sea scanning for vessels). The other is mounted on a rooftop, pointed at streets and buildings. But at the signal processing level, they are doing something surprisingly similar---and that similarity is the foundation of ISAC.

## What a radar actually does

A radar works on a simple principle: you transmit a signal (one you designed and know exactly), and that signal travels outward, hits an object, and some fraction of the energy reflects back. You receive the echo, compare it to what you originally sent, and from that comparison you can infer three things: how far away the object is (from the round-trip delay), how fast it is moving (from the Doppler frequency shift), and roughly what direction it came from (from the angle of arrival at your antenna array).

The key is that reference. Because you know what you transmitted, any deviation in the echo is signal, not noise. The delay tells you range. The frequency shift tells you velocity. The angle tells you direction. Radar is, at its core, *matched filtering* applied to a known waveform.

<!-- IMAGE PROMPT for fig1-radar-principle.png | place file at /images/posts/isac/fig1-radar-principle.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8), amber (#FFB347).

Horizontal diagram showing radar operation. Left side: a radar dish or antenna icon in electric blue. A transmitted signal pulse (glowing electric blue arrow) travels to the right toward a simple geometric target (small car or aircraft silhouette in white outline at center). A reflected echo signal (glowing cyan dashed arrow) curves back from the target toward the radar on the left. Below the diagram: three small annotation boxes in dark slate with white bold text: "Delay -> Range", "Doppler shift -> Velocity", "Angle of arrival -> Direction". The annotation boxes are connected by thin white lines to corresponding parts of the echo path. Faint dot-grid background. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/isac/fig1-radar-principle.png" alt="Diagram of radar operation: a transmitted signal bounces off a target and the echo encodes range, velocity, and direction" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">Radar extracts environmental information---range, velocity, direction---by comparing a known transmitted signal against its received echo.</figcaption>
</figure>

## A base station already does most of this

Now think about what a base station does during channel estimation. It transmits a known pilot signal---a reference sequence both transmitter and receiver know in advance. The receiver measures what arrived and compares it to what was sent. From that comparison, it estimates how the channel distorted the signal: which paths exist, at what delays and angles, with what amplitudes.

That channel estimate is, implicitly, a description of the physical environment. The delay spread tells you something about the distances to the dominant scatterers. The angle of arrival tells you something about where objects are relative to the base station. The base station is already doing something structurally similar to radar---it is just using that information only for equalization, not for sensing.

The hardware prerequisites are largely in place. Wide bandwidth gives you range resolution---the finer the bandwidth, the shorter the delay differences you can distinguish, and therefore the more precise your range estimate. A massive MIMO antenna array gives you angular resolution---the more antennas, the narrower the spatial beams you can form, and the more precisely you can locate a scatterer. 5G base stations, deployed right now, have both of these.

So why is ISAC a 6G feature rather than a 5G one? Partly standardization: sensing was not designed into the 5G specification. But more fundamentally, a 5G base station was not designed with sensing in mind. Its waveform, pilot structure, and resource allocation are all optimized for communication. Using it for sensing is possible, but you are working against some of its design choices rather than with them.

---

## The constraint you cannot escape

A dedicated radar engineer has a freedom that a base station does not: the freedom to choose the waveform. Want better range resolution? Use a wider bandwidth chirp. Want to suppress range-Doppler ambiguity? Carefully design the pulse repetition interval. The waveform IS the radar's primary design variable.

A base station must transmit OFDM, because that is what its users expect. OFDM happens to work reasonably for sensing---the subcarrier structure gives you a natural time-frequency grid for delay-Doppler estimation, and you can extract channel information subcarrier by subcarrier. But "happens to work" is different from "designed for it." Certain sensing tasks---detecting slow-moving targets in high-clutter environments, for example---are hard with OFDM in ways they would not be with a purpose-built radar waveform.

The analogy is something like this. Imagine someone who is an excellent musician asked to also take phone calls during a performance. They can do it. They may even handle both surprisingly well during quiet passages. But their attention is divided, and there will be moments where one task suffers for the other. A base station serving dense, high-traffic areas has limited spare capacity for sensing. A base station in a lightly loaded cell, with idle resource blocks and guard intervals, has much more headroom.

This is actually the intuition behind one of ISAC's more defensible use cases: using the "quiet time" (unused slots, guard periods, idle bandwidth) for sensing at essentially zero comms cost. You are not competing with your primary job if there is no primary job happening at that moment.

<!-- IMAGE PROMPT for fig2-isac-base-station.png | place file at /images/posts/isac/fig2-isac-base-station.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8), amber (#FFB347).

Center: a base station tower icon with a massive MIMO antenna array, glowing electric blue. From the base station, two types of signals radiate simultaneously: narrow electric blue directional beam wedges pointing downward-left and downward-right toward two small smartphone user icons (communications beams). Separately, a wider cyan sensing beam points upward-right toward a small car icon driving along a road silhouette, with a dashed echo line returning from the car back to the base station (sensing echo in amber). A subtle split-focus visual effect on the base station---perhaps a faint dividing line or dual glow---suggests the station is doing two things at once. Faint dot-grid background. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/isac/fig2-isac-base-station.png" alt="A base station simultaneously serving communication users with directional beams while sensing a moving vehicle with a separate sensing beam and receiving its echo" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">An ISAC base station allocates some of its resources to serving users (communications) and some to illuminating and receiving echoes from the environment (sensing). The challenge is that those resources are shared.</figcaption>
</figure>

---

## Where the value actually is

If a dedicated radar is better at sensing---which it generally is---why build ISAC at all? There are two arguments that hold up under scrutiny.

**The infrastructure argument.** A radar network with the density of a cellular network would be staggering to deploy. Every city block, every indoor space, every industrial floor---blanketed with dedicated sensing hardware. The economics do not work for most applications. A 6G network, by contrast, will be deployed for communications reasons regardless. If each base station also senses, you get ubiquitous environmental awareness as a consequence of infrastructure that was going to exist anyway. The sensing might be lower quality than a dedicated radar, but its coverage is city-scale by default. That trade-off is worth taking seriously.

**The synergy argument.** A standalone radar produces data---tracks of objects, maps of the environment---that then has to be transmitted to, processed by, and acted upon by some other system. In a cellular network, the sensing output can feed directly back into the communications system that generated it. Know where users are? Predict their beam before they move. Know there is a truck blocking a propagation path? Anticipate the shadow fading and adapt the link. The environment map is not a separate product delivered to a separate customer---it is an input to the comms system's own operations. This closed-loop synergy has no analogue in standalone radar.

Taken together, these two arguments describe a scenario where ISAC is compelling not because it is a great radar, but because it is a good-enough sensor at a scale and integration depth that no dedicated sensor network can match.

---

## But be careful about the hype

Compared to a purpose-built radar system, an ISAC system will generally have worse sensing performance for a given hardware budget. The waveform is constrained. The antenna geometry is chosen for communications coverage, not radar cross-section optimization. Interference between the sensing and communications functions---particularly in multi-cell environments---is a real and open problem. And the privacy implications of pervasive, always-on environmental sensing embedded in the communications network are not trivial.

There is also a more subtle issue. Some of the most cited ISAC use cases---high-accuracy localization, gesture recognition, indoor mapping---require sensing quality that an ISAC system may not reliably deliver, especially in loaded networks where comms traffic leaves little room for sensing. The cases where ISAC clearly wins are the ones where moderate sensing quality, deployed everywhere, beats excellent sensing quality deployed somewhere. Not every application fits that description.

---

## The engineering goes deeper than one post can cover

This post has only sketched the shape of the argument. The actual engineering of an ISAC system---how you design waveforms that trade off comms and sensing performance, how you allocate resources between the two functions, how multiple ISAC nodes cooperate to form a distributed sensor array, what the fundamental limits look like---is a deep research area. So is the question of when ISAC's value proposition holds up under rigorous system-level analysis, and when a hybrid deployment of simpler dedicated sensors alongside the base station would just be more practical.

A proper treatment of ISAC's strengths, weaknesses, open research directions, and realistic deployment scenarios deserves its own post---one that goes further into the technical mechanics rather than staying at the conceptual level.

For now, the short version: ISAC is one of 6G's most interesting bets. The hardware prerequisites are largely there. The value proposition for ubiquitous infrastructure sensing and comms-sensing synergy is real. But it will need honest benchmarking against alternatives---not just against other ISAC designs, but against the question of whether a standalone sensor network, or a hybrid approach, would serve the use case better.

---

*Next in the series: **Ubiquitous Connectivity**---what it means for 6G to extend coverage beyond where cell towers are economical to build, and why satellites and aerial platforms are part of that answer.*

---

### References

\[1\] ITU-R, "Framework and overall objectives of the future development of IMT for 2030 and beyond," Recommendation ITU-R M.2160, International Telecommunication Union, Geneva, Nov. 2023. [Online]. Available: <https://www.itu.int/rec/R-REC-M.2160/en>

\[2\] F. Liu, C. Masouros, A. P. Petropulu, H. Griffiths, and L. Hanzo, "Joint radar and communication design: Applications, state-of-the-art, and the road ahead," *IEEE Transactions on Communications*, vol. 68, no. 6, pp. 3834--3862, Jun. 2020.

\[3\] C. Sturm and W. Wiesbeck, "Waveform design and signal processing aspects for fusion of wireless communications and radar sensing," *Proceedings of the IEEE*, vol. 99, no. 7, pp. 1236--1259, Jul. 2011.

\[4\] A. Liu et al., "A survey on fundamental limits of integrated sensing and communication," *IEEE Communications Surveys & Tutorials*, vol. 24, no. 2, pp. 994--1034, 2022.
