---
layout: page
title: LLM Refusal Geometry
description: Empirical study on whether random-vector jailbreaks engage or bypass the refusal direction in LLMs
img: assets/img/Research_Project.png
importance: 4
category: research
related_publications: false
---

<div style="border-left: 4px solid #f0ad4e; background: #fff8f0; padding: 0.8rem 1.2rem; margin-bottom: 1.5rem; border-radius: 0 4px 4px 0;">
  <strong>Work in progress.</strong> This page describes ongoing research. Results are preliminary and the analysis is not complete. I will update this page when the preprint is available.
</div>

This is a solo undergraduate research project targeting a NeurIPS 2026 workshop submission. The question bridges two of the most-cited mechanistic interpretability results from 2024 and 2025.

**Background.** Arditi et al. (2024) showed that safety-tuned LLMs have a "refusal direction" in their residual stream — a single linear direction whose activation strongly predicts whether the model will refuse a harmful request. Ablating or steering along this direction can suppress refusal almost entirely. The implication, widely repeated, is that refusal is geometrically simple: it lives in a one-dimensional subspace of the model's representation space.

Separately, Siddiqui et al. (2025) showed that random vectors added to a model's weights can jailbreak it at surprisingly high rates, with no gradient-based optimization. The vectors are not targeted at anything specific.

**The question.** Do these random-vector jailbreaks work by pushing activations through the refusal direction, or do they bypass it entirely? If the jailbreaks correlate with projection onto the refusal direction, that would support the single-direction hypothesis. If they do not correlate, it suggests refusal is more distributed than the Arditi result implies, and that random perturbations are finding a different path around safety training.

**Preliminary result.** The scatter plot below shows jailbreak rate against projection magnitude onto the refusal subspace across thousands of random vectors, run on Llama 3.1 8B.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/Research_Project.png" alt="Scatter plot of jailbreak rate vs. refusal subspace projection (Llama 3.1 8B)" style="max-width: 640px; width: 100%;">
</div>

The Spearman correlation is essentially zero (ρ = -0.004). The preliminary reading is that random-vector jailbreaks are not engaging the refusal direction at all, which would push back on the single-direction view of refusal. Full analysis, additional models, and ablations are in progress.
