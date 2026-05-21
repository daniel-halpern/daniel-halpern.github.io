---
layout: page
title: Vox PopulAI
description: Simulating electorates in 6D ideological space to predict voting behavior on any policy
img: assets/img/AI_Electorate_Simulator.png
importance: 1
category: projects
related_publications: false
---

Built at a hackathon, Vox PopulAI is a full-stack simulator that takes a demographic description and a policy proposal, generates a synthetic electorate of AI citizens, and runs a mathematical voting simulation against them. The core premise is that standard polling reduces voters to a single label like "liberal" or "conservative," which loses most of the actual signal. This tries a different approach: represent every citizen as a point in a 6-dimensional ideological space and calculate their vote geometrically.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/AI_Electorate_Simulator.png" alt="Vox PopulAI dashboard" style="max-width: 700px; width: 100%;">
</div>

The six axes are Economic, Social, Environmental, Authority, Collectivism, and Risk, each a continuous value in a bounded range. Every citizen gets a unique 6D vector, their ideological fingerprint, which can capture internal contradictions: someone economically conservative but socially progressive sits in a part of the space that a 1D left-right scale cannot express.

I use Gemini not as a chatbot but as a structured data engine. Given a demographic string like "50% union workers in Ohio, 20% college students," it returns a JSON array of citizen objects with valid 6D vectors, not prose. The tricky part was forcing the model to produce realistic distributions. When you ask an LLM to generate "Republicans" and "Democrats," it plots them in a mathematically boring straight line. I had to engineer the system prompt to enforce Gaussian variance and require internal contradictions, so the output looks like a real messy blob of human opinions rather than a tidy ideological spectrum.

Once the electorate exists, you propose a policy. Gemini maps the policy text onto its own 6D vector. Then the voting simulation runs entirely in TypeScript: for each citizen, I compute the Euclidean distance between their vector and the policy vector, run it through a sigmoid function to get a support probability, then calculate turnout based on how far from neutral that citizen sits. Citizens who strongly love or hate the policy show up. Indifferent citizens stay home at roughly 40% turnout, matching observed patterns.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/AI_Electorate_clustering.png" alt="K-Means faction clustering in 3D" style="max-width: 700px; width: 100%;">
</div>

The results render as an interactive 3D scatter plot. Since 6D does not display on a monitor, I compress to 3 axes (Economic, Social, Authority) for the visual while keeping all 6 in the math. K-Means clustering runs on the full 6D data and assigns citizens to emergent factions, which Gemini names based on each cluster's centroid. I did not define any parties ahead of time. A simulation of Ohio factory workers produces entirely different factions than one of Bay Area tech workers, and both tend to feel plausible.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/AI_Electorate_results.png" alt="Simulation vote results" style="max-width: 700px; width: 100%;">
</div>

One calibration problem I had to fix: early versions treated every policy as divisive. "Provide clean drinking water to children" would still return 40% opposition because some citizens happened to be geometrically distant from its ideology vector. The math was technically correct but the result was absurd. I added a universal appeal modifier where Gemini evaluates whether a policy has inherent valence and shifts the probability curve accordingly, so common-sense policies can reach realistic supermajorities.

The most satisfying moment in the whole project was typing "Elect Donald Trump" into the policy field. The simulation returned over 50% support, which matches his 2024 popular vote result. I did not hardcode that. The 6D geometry and the Gemini-generated electorate arrived at it independently.

Other pieces: ElevenLabs synthesizes voice for individual citizen chat sessions, so you can click any dot on the 3D map and have a voice conversation with that simulated voter. Snowflake logs every simulation run across all users and powers a global analytics dashboard. Solana writes finalized poll results on-chain as an immutable record.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/AI_Electorate_global_stats.png" alt="Global Snowflake analytics dashboard" style="max-width: 700px; width: 100%;">
</div>

[View on GitHub](https://github.com/daniel-halpern/AI-Electorate-Simulator)
