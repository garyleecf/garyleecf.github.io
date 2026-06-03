---
layout: single
title: "Uncovering Hidden Structures in Wireless Systems with AI"
date: 2026-04-08
categories:
  - 6G
tags:
  - Machine Learning
  - Data-Driven
  - Wireless
  - Channel Estimation
  - AI-Native
excerpt: "Wireless systems have been built on a Gaussian approximation for decades. At higher frequencies, that approximation starts to cost something real. AI-native 6G is, in part, a proposal to uncover and take advantage of the hidden structure."
author_profile: true
---

Last post, I described the six usage scenarios that define 6G---the three evolved service classes from 5G, and three new ones: **Integrated Sensing and Communication (ISAC)**, **AI and Communication**, and **Ubiquitous Connectivity**. This post is the first of three going deeper on each. I am starting with *AI and Communication*, partly because it sits closest to my own research, and partly because it is the scenario that most directly challenges how wireless systems have been built for the last several decades.

The ITU's framing---*AI and Communication*, not "AI for communication"---is intentional. The proposition is not that AI will enhance a communication network from the outside. It is that AI becomes part of the design fabric of the network itself. What does that actually mean in practice?

The short version: some of the assumptions wireless systems were built on are worth revisiting. They are not wrong exactly---they are simplifications that kept the mathematics tractable, and they served the field well. But at millimetre-wave frequencies, where a significant share of 6G's performance ambitions live, those simplifications start to cost something real and measurable. AI-native design is, in part, a proposal to stop leaving that performance on the table.

---

## Simplification in our comfort zone

When a signal travels through the air, it doesn't go point to point. It scatters---bounces off buildings, diffracts around corners, reflects off vehicles, gets absorbed by foliage. By the time it arrives at the receiver, it has come via dozens of paths, each at a slightly different angle, slightly different delay, slightly different amplitude.

<!-- IMAGE PROMPT for fig1-multipath.png | place file at /images/posts/ai-native-6g/fig1-multipath.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8).

A wireless transmitter (small antenna tower icon, electric blue glow, left side) and a receiver (small smartphone icon, cyan glow, right side). Between them, multiple signal paths: one straight direct line-of-sight path in bright electric blue. Two or three reflected paths in cyan that curve and bounce off simple rectangular building silhouettes (thin white-line outlines, dark filled). One path visibly diffracts around a building corner as a gentle arc. Each path is a glowing arrow-tipped line. The paths arrive at the receiver from slightly different angles, suggesting the multipath effect. Faint dot-grid overlay on background. No text. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/ai-native-6g/fig1-multipath.png" alt="Diagram showing a wireless signal traveling from transmitter to receiver via multiple scattered paths, representing multipath propagation" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">A signal traveling through a real environment does not take a single path. Scattering, reflection, and diffraction produce a superposition of many arrivals at the receiver.</figcaption>
</figure>

Characterising that precisely is, in general, very hard. So classical theory made a practical decision: if you have many independent random contributions summing together, invoke the central limit theorem, and the aggregate looks Gaussian. White noise. Rayleigh fading. A handful of parameters. Tractable mathematics.

This is an impressive piece of reasoning, and it has been extraordinarily productive. Shannon capacity, optimal receiver design, error-correcting codes---most of what we actually deploy runs on Gaussian foundations.

But it is still an approximation. And as we push into millimetre-wave frequencies---where a lot of 6G's ambition for high-throughput links lives---that approximation starts to cost us something real.

---

## The channel that gets simpler and stranger at the same time

Here is something that surprises people when they first encounter it. You might expect that going to higher frequencies makes the wireless channel more chaotic. More reflections, more unpredictability. In fact, it goes the other way.

At millimetre-wave, signals attenuate aggressively. Most of those scattered bounces just disappear. What you are left with is a small number of dominant propagation paths---a line-of-sight component if you are lucky, a strong reflection off a nearby surface, and then basically nothing. The channel is *sparse* in the angular domain. Energy arrives from a few directions, not all of them.

<!-- IMAGE PROMPT for fig2-sparse-channel.png | place file at /images/posts/ai-native-6g/fig2-sparse-channel.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8).

Two side-by-side top-down diagrams of a base station radiating signals, divided by a thin white vertical line. Left panel: many thin overlapping signal rays (15 to 20) radiating outward in nearly all directions from a central antenna icon, in muted cyan of roughly equal intensity---represents rich multipath at sub-6GHz. Right panel: only 2 to 3 prominent sharp directional beams radiating from the same antenna icon in bright electric blue with a glow effect; the majority of directions are empty and dark---represents a sparse mmWave channel. Faint dot-grid background. No text. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/ai-native-6g/fig2-sparse-channel.png" alt="Comparison of sub-6GHz rich multipath (many signal rays in all directions) versus mmWave sparse channel (2-3 dominant directional beams)" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">At sub-6GHz frequencies, energy arrives from many directions simultaneously (left). At millimetre-wave, higher path loss strips away most reflections, leaving only a handful of dominant propagation paths (right).</figcaption>
</figure>

This is not a messier channel. It is, in a meaningful sense, a more structured one.

The problem is that a Gaussian model does not know this. It has no prior that says energy should be concentrated in any particular direction. It treats all angles equally. It is like trying to find a face in a photograph by averaging over every possible configuration of pixels---technically defensible, practically wasteful.

The performance cost shows up most clearly in how the network designs its *codebook*---the set of beams it uses to serve users across a cell.

---

## A concrete example: the codebook problem

In a massive MIMO system, the base station does not broadcast in all directions at once. It forms focused beams and allocates them to users. The collection of beams it can choose from is the codebook.

The uninformed approach is to spread those beams uniformly across all possible angles. If a user could be *anywhere*, cover everything equally. That is fig. 3a---twelve beams, evenly spaced, no assumptions made about the world.

Now add the environment. Users are in buildings, on streets, in corridors. The geometry constrains where they actually are. Some angular directions from any given base station are simply not accessible---blocked by a wall, a building, a car park. That is fig. 3b. The codebook has not changed, but now it is obvious that some beams are pointing at regions where no user will ever be. Those are wasted degrees of freedom---capacity you paid for and cannot use.

Fig. 3c is where it gets interesting. Same number of beams, but now shaped around where users can actually be. The inaccessible zones get nothing. The accessible ones get finer angular resolution, tighter beams, better spatial separation between users. The codebook has not grown; it has been *informed*.

<!-- IMAGE PROMPT for fig3-codebook.png | place file at /images/posts/ai-native-6g/fig3-codebook.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8), amber (#FFB347).

Three side-by-side top-down diagrams (3a, 3b, 3c), each showing a small base station icon at center with beam sectors radiating outward. Thin white vertical lines separate the three panels.

Panel 3a (left): 12 uniform triangular beam sectors evenly distributed 360 degrees around the base station, all equal-width electric blue wedges---uniform codebook, no assumptions.

Panel 3b (center): Same 12 beams as 3a. Three or four sectors are filled with a dark opaque overlay representing inaccessible zones blocked by solid dark rectangular building silhouettes around the perimeter. The blocked beam sectors are muted and dark; the accessible sectors are in cyan.

Panel 3c (right): Beams redistributed. The inaccessible zones receive no beams. The accessible zones receive more beams with narrower, finer angular resolution wedges packed closely, in bright cyan with a glow, and amber highlights on the most prominent beams---an informed codebook shaped by real geometry.

No text. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/ai-native-6g/fig3-codebook.png" alt="Three top-down beam codebook diagrams: (a) uniform beams in all directions, (b) same beams with inaccessible zones shown, (c) beams redistributed and concentrated in accessible directions" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;"><strong>Left:</strong> A uniform codebook makes no assumptions about the environment. <strong>Center:</strong> In practice, a portion of those beams point into regions no user can reach. <strong>Right:</strong> An informed codebook concentrates angular resolution where it is actually needed.</figcaption>
</figure>

The performance difference between a uniform and an informed codebook is not small. In dense urban deployments, it translates directly into how many users a cell can serve simultaneously---the kind of gain that shows up in system-level throughput, not just in link-level simulations [3]. The question is how you get the informed version. You could derive it analytically if you have a sufficiently accurate model of the environment. But real environments are messy, partial, and irregular---the clean analytical derivation gets complicated quickly. The increasingly practical answer is to learn it.

---

## Structure you can learn without being able to describe

Learned estimators sidestep the commitment that compressed sensing requires, and this is where the argument connects back to the non-Gaussian point.

If you know the channel is sparse, you can exploit it directly. Compressed sensing algorithms---matching pursuit, LASSO---recover sparse signals from far fewer measurements than a Gaussian estimator would require. You don't need to probe every direction if you know most directions are empty. This idea has been influential in 5G channel estimation research [2].

But compressed sensing requires you to specify the sparsity structure: which basis the channel is sparse in, how sparse, what the noise model looks like. Get those wrong and the gains evaporate. Real millimetre-wave channels are sparse in ways that are approximately but not exactly what a textbook model says---the support varies with environment, there are correlations across antenna arrays that the standard basis ignores.

A learned estimator sidesteps this commitment. Train a neural network on empirical channel data from the actual deployment---the real buildings, the real mobility patterns, the real interference---and it absorbs the statistical structure of that environment without requiring you to write it down analytically. It learns that energy arrives from *these* angular ranges, in *these* cluster shapes. Not because you specified it. Because the data showed it.

The adapted codebook in fig. 3c is one illustration of the same principle. But the logic extends to channel estimation, CSI compression, beam management---anywhere the system currently makes a Gaussian assumption and pays a performance tax for it.

---

## Why this is an architecture problem, not just an algorithm problem

Here is the part that often gets skipped over, and it matters.

The interface contracts between layers of the communications stack were designed around the Gaussian assumption---what the physical layer measures and reports, what the UE feeds back to the base station, what the channel model looks like to the scheduler. Pilot structures, feedback codebook formats, link adaptation curves: most of it was dimensioned for a particular model of what channels look like.

<!-- IMAGE PROMPT for fig4-stack.png | place file at /images/posts/ai-native-6g/fig4-stack.png

Tech blog illustration in wide landscape format (3:2 ratio, 1536x1024 px). Dark navy background (#0D1B2A). Flat vector art with subtle neon glow effects. Accent colors: electric blue (#00B4D8), bright cyan (#06FFE8), amber (#FFB347).

Center of image: a vertical protocol stack---5 horizontal rounded-rectangle layers stacked from bottom to top. Each layer has a short bold white sans-serif label centered inside it. From bottom to top the labels read: "PHY", "MAC", "RLC", "PDCP", "Application". The bottom two layers (PHY and MAC) have a warm amber glow around their borders and a slightly brighter interior, indicating where classical Gaussian assumptions are embedded. The top three layers are in muted dark slate with minimal glow and their labels in lighter gray.

On the left side of the stack, a thin amber vertical bracket spans the PHY and MAC layers with a small bold white label beside it reading "How to go beyond Gaussian assumptions". On the right side, thin bright cyan arrows point inward toward the PHY and MAC layers with a glow effect, with a small bold white label reading "AI-native redesign". Thin white connecting arrows between adjacent layers on the right edge of the stack show internal interfaces.

Clean, symmetric, legible text. Faint dot-grid background. 1536x1024 landscape.
-->
<figure style="margin: 1.8em 0 1.4em;">
  <img src="/images/posts/ai-native-6g/fig4-stack.png" alt="Communications protocol stack diagram with the physical and MAC layers highlighted as the location of Gaussian assumptions, and AI-native redesign indicated at those layers" style="max-width: 100%;"/>
  <figcaption style="text-align: center; font-size: 0.82em; color: #7A6858; margin-top: 0.5em;">The classical Gaussian assumption is baked into the lower layers of the stack---pilot structures, feedback formats, link adaptation curves. An AI-native system redesigns those interfaces, not just the algorithms running above them.</figcaption>
</figure>

If you swap in a better estimator but leave those interfaces unchanged, you recover some performance. But you are still operating through specifications built for a different world. An AI-native system is one where those interface contracts are redesigned from the ground up around the assumption that learned representations will be doing the heavy lifting. Change the estimator *and* the contract, and the gains compound.

This is the architectural claim in IMT-2030's *AI and Communication* scenario. The network is not getting a smarter add-on. It is being rethought from the physical layer up, around the premise that the old approximations were holding it back.

---

## What this enables

The practical consequence is a network that adapts to its actual environment rather than a textbook approximation of it.

Conventional systems are designed to worst-case specifications---dimensioned for a channel that could be anywhere in the space the Gaussian model defines. A system that has learned the real distribution of channels in its deployment can afford to be more aggressive: finer codebooks, more targeted estimation, beam management tuned to local geometry. In dense urban millimetre-wave deployments, where the channel is sparse and structured, the gap between *designed-for-the-model* and *designed-for-the-reality* is large and exploitable.

The deeper point is about information. Real channels carry more structure than Gaussian models capture. A system built to learn and exploit that structure gets more performance from the same spectrum and hardware---not because it is more powerful, but because it has stopped making assumptions that were never quite true.

That is the AI-native proposition. Not AI as a layer on top of a classical system. AI as the thing that finally lets the network close the gap between the world it was designed for and the world it actually operates in.

---

*Next in the series: the other two new 6G scenarios---what it means for a network to also be a sensor (**ISAC**), and how 6G plans to extend coverage to places a cell tower was never economical to build (**Ubiquitous Connectivity**).*

---

### References

\[1\] ITU-R, "Framework and overall objectives of the future development of IMT for 2030 and beyond," Recommendation ITU-R M.2160, International Telecommunication Union, Geneva, Nov. 2023. [Online]. Available: <https://www.itu.int/rec/R-REC-M.2160/en>

\[2\] W. U. Bajwa, J. Haupt, A. M. Sayeed, and R. Nowak, "Compressed channel sensing: A new approach to estimating sparse multipath channels," *Proceedings of the IEEE*, vol. 98, no. 6, pp. 1058--1076, Jun. 2010.

\[3\] A. Alkhateeb, O. El Ayach, G. Leus, and R. W. Heath, "Channel estimation and hybrid precoding for millimeter wave cellular systems," *IEEE Journal of Selected Topics in Signal Processing*, vol. 8, no. 5, pp. 831--846, Oct. 2014.
