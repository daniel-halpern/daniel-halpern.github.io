---
layout: page
title: ML Sandbox
description: From-scratch PyTorch implementations of everything from linear regression to transformers
img: assets/img/ML_sandbox.png
importance: 4
category: projects
related_publications: false
---

<div style="border-left: 4px solid #f0ad4e; background: #fff8f0; padding: 0.8rem 1.2rem; margin-bottom: 1.5rem; border-radius: 0 4px 4px 0;">
  <strong>Work in progress.</strong> New modules are added over time as the series continues.
</div>

ML Sandbox is a self-contained collection of PyTorch notebooks that walks through the core ML architectures in roughly historical order, from linear models to transformers. The goal is to give someone starting out a clear progression where each module builds on the last, and to give myself a reference I can actually return to. Rather than pulling in high-level libraries, each concept is implemented from scratch so the mechanics stay visible.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/ML_sandbox.png" alt="Nonlinear decision boundary learned by a neural network" style="max-width: 600px; width: 100%;">
</div>

The sequence so far, with more planned:

1. Linear models and regression
2. Nonlinear classification with MLPs and activation functions
3. Training dynamics (optimizers, learning rate schedules, regularization)
4. CNNs on MNIST
5. Representation learning — what the network's latent space actually looks like
6. *(Planned)* RNNs and sequence models
7. *(Planned)* Attention mechanisms and transformers
8. *(Planned)* Mini GPT

The through-line is the idea that every architecture is solving the same problem of turning raw input into a useful representation, just with different assumptions about structure. A CNN bakes in spatial locality. An RNN bakes in sequential order. A transformer makes no assumptions and just learns which parts of the input to attend to.

