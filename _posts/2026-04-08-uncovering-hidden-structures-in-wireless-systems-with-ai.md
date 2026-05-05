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

AI is everywhere right now. AI is pervasive, changing ways we do things in many places.
Even in wireless communications, we are seeing various strategies and approaches to integrating AI.
Recent efforts make a distinction between having AI introduced as an after thought to enhance/improve results, as opposed to "AI-Native", i.e., how to fundametnally change the ways we do things when we redesign certain things with AI.

What does this really mean? Where does that AI reside and what does it actually do? 

Rather than thinking of it as some chatGPT trying to explain parts of the network, AI in 6G presents opportuntiies that are more fundamental, and might also challenge the classical way we treat communications systems. The IMT-2030 framework — the ITU's blueprint for what 6G is supposed to be — includes a scenario called *AI and Communication*, in that AI becomes central and native to communication design. The phrasing is likely to be a conscious choice, and I hope to shine some light into where such opportunities could arise.

The short version: some of the assumptions we built wireless systems on for the last several decades ought to be revisited. They are not necessarily wrong, but more like they might be simplifications or abstractions that we were comfortable. But to squeeze out more performance and to really reach the next level, we may want to address this "beast" hiding behind hidden structures. AI-native 6G is, in part, a proposal to stop living with it.

---

## Simplification in our comfort zone

When a signal travels through the air, it doesn't go point to point. It scatters — bounces off buildings, diffracts around corners, reflects off vehicles, gets absorbed by foliage. By the time it arrives at the receiver, it has come via dozens of paths, each at a slightly different angle, slightly different delay, slightly different amplitude.

{% include posts/ai-native-6g/fig1_multipath.html %}

Characterising that precisely is, in general, very hard. So classical theory made a practical decision: if you have many independent random contributions summing together, invoke the central limit theorem, and the aggregate looks Gaussian. White noise. Rayleigh fading. A handful of parameters. Tractable mathematics.

This is a genuinely impressive piece of reasoning, and it has been extraordinarily productive. Shannon capacity, optimal receiver design, error-correcting codes — a huge fraction of what we actually deploy runs on Gaussian foundations.

But it is still an approximation. And as we push into millimetre-wave frequencies — where a lot of 6G's ambition for high-throughput links lives — that approximation starts to cost us something real.

---

## The channel that gets simpler and stranger at the same time

Here is something that surprises people when they first encounter it. You might expect that going to higher frequencies makes the wireless channel more chaotic. More reflections, more unpredictability. In fact, it goes the other way.

At millimetre-wave, signals attenuate aggressively. Most of those scattered bounces just disappear. What you are left with is a small number of dominant propagation paths — a line-of-sight component if you are lucky, a strong reflection off a nearby surface, and then basically nothing. The channel is *sparse* in the angular domain. Energy arrives from a few directions, not all of them.

{% include posts/ai-native-6g/fig2_sparse_channel.html %}

This is not a messier channel. It is, in a meaningful sense, a more structured one.

The problem is that a Gaussian model does not know this. It has no prior that says energy should be concentrated in any particular direction. It treats all angles equally. It is like trying to find a face in a photograph by averaging over every possible configuration of pixels — technically defensible, practically wasteful.

The performance cost shows up most clearly in how the network designs its *codebook* — the set of beams it uses to serve users across a cell.

---

## A concrete example: the codebook problem

In a massive MIMO system, the base station does not broadcast in all directions at once. It forms focused beams and allocates them to users. The collection of beams it can choose from is the codebook.

The uninformed approach is to spread those beams uniformly across all possible angles. If a user could be *anywhere*, cover everything equally. That is fig. 3a — twelve beams, evenly spaced, no assumptions made about the world.

Now add the environment. Users are in buildings, on streets, in corridors. The geometry constrains where they actually are. Some angular directions from any given base station are simply not accessible — blocked by a wall, a building, a car park. That is fig. 3b. The codebook has not changed, but now it is obvious that some beams are pointing at regions where no user will ever be. Those are wasted degrees of freedom — capacity you paid for and cannot use.

Fig. 3c is where it gets interesting. Same number of beams, but now shaped around where users can actually be. The inaccessible zones get nothing. The accessible ones get finer angular resolution, tighter beams, better spatial separation between users. The codebook has not grown; it has been *informed*.

{% include posts/ai-native-6g/fig3_codebook.html %}

The performance difference between a uniform and an informed codebook is not a rounding error. In dense urban deployments it translates directly into how many users a cell can serve simultaneously. The question is how you get the informed version. You could derive it analytically if you have a sufficiently accurate model of the environment. But real environments are messy, partial, irregular — the clean analytical derivation gets complicated quickly. The increasingly practical answer is to learn it.

---

## Structure you can learn without being able to describe

This is where sparse recovery and learned models come in, and where the argument connects back to the non-Gaussian point.

If you know the channel is sparse, you can exploit it directly. Compressed sensing algorithms — matching pursuit, LASSO — recover sparse signals from far fewer measurements than a Gaussian estimator would require. You don't need to probe every direction if you know most directions are empty. This idea has been influential in 5G channel estimation research.

But compressed sensing requires you to specify the sparsity structure: which basis the channel is sparse in, how sparse, what the noise model looks like. Get those wrong and the gains evaporate. Real millimetre-wave channels are sparse in ways that are approximately but not exactly what a textbook model says — the support varies with environment, there are correlations across antenna arrays that the standard basis ignores.

A learned estimator sidesteps this commitment. Train a neural network on empirical channel data from the actual deployment — the real buildings, the real mobility patterns, the real interference — and it absorbs the statistical structure of that environment without requiring you to write it down analytically. It learns that energy arrives from *these* angular ranges, in *these* cluster shapes. Not because you specified it. Because the data showed it.

The adapted codebook in fig. 3c is one illustration of the same principle. But the logic extends to channel estimation, CSI compression, beam management — anywhere the system currently makes a Gaussian assumption and pays a performance tax for it.

---

## Why this is an architecture problem, not just an algorithm problem

Here is the part that often gets skipped over, and it matters.

The interface contracts between layers of the communications stack — what the physical layer measures and reports, what the UE feeds back to the base station, what the channel model looks like to the scheduler — were all designed around the Gaussian assumption. Pilot structures, feedback codebook formats, link adaptation curves: all of it was dimensioned for a particular model of what channels look like.

{% include posts/ai-native-6g/fig4_stack.html %}

If you swap in a better estimator but leave those interfaces unchanged, you recover some performance. But you are still operating through specifications built for a different world. An AI-native system is one where those interface contracts are redesigned from the ground up around the assumption that learned representations will be doing the heavy lifting. Change the estimator *and* the contract, and the gains compound.

This is the architectural claim in IMT-2030's *AI and Communication* scenario. The network is not getting a smarter add-on. It is being rethought from the physical layer up, around the premise that the old approximations were holding it back.

---

## What this enables

The practical consequence is a network that adapts to its actual environment rather than a textbook approximation of it.

Conventional systems are designed to worst-case specifications — dimensioned for a channel that could be anywhere in the space the Gaussian model defines. A system that has learned the real distribution of channels in its deployment can afford to be more aggressive: finer codebooks, more targeted estimation, beam management tuned to local geometry. In dense urban millimetre-wave deployments, where the channel is genuinely sparse and structured, the gap between *designed-for-the-model* and *designed-for-the-reality* is large and exploitable.

The deeper point is about information. Real channels carry more structure than Gaussian models capture. A system built to learn and exploit that structure gets more performance from the same spectrum and hardware — not because it is more powerful, but because it has stopped making assumptions that were never quite true.

That is the AI-native proposition. Not AI as a layer on top of a classical system. AI as the thing that finally lets the network close the gap between the world it was designed for and the world it actually operates in.

---

*Next in the series: we get specific — **channel estimation with neural networks**, what it actually looks like in practice, and how learned estimators compare to classical baselines like MMSE.*

---

### References

\[1\] ITU-R, "Framework and overall objectives of the future development of IMT for 2030 and beyond," Recommendation ITU-R M.2160, International Telecommunication Union, Geneva, Nov. 2023. [Online]. Available: <https://www.itu.int/rec/R-REC-M.2160/en>

\[2\] W. U. Bajwa, J. Haupt, A. M. Sayeed, and R. Nowak, "Compressed channel sensing: A new approach to estimating sparse multipath channels," *Proceedings of the IEEE*, vol. 98, no. 6, pp. 1058–1076, Jun. 2010.

\[3\] A. Alkhateeb, O. El Ayach, G. Leus, and R. W. Heath, "Channel estimation and hybrid precoding for millimeter wave cellular systems," *IEEE Journal of Selected Topics in Signal Processing*, vol. 8, no. 5, pp. 831–846, Oct. 2014.
