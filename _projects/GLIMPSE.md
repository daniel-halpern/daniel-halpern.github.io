---
layout: page
title: GLIMPSE
description: MATLAB GUI for single-molecule fluorescence analysis in TIRF microscopy
img: assets/img/GLIMPSE.png
importance: 1
category: research
related_publications: false
---

GLIMPSE (Gradinaru Lab sIngle Molecule Photobleaching analySis interfacE) is a MATLAB App Designer GUI for the Gradinaru Lab that extracts fluorophore intensity traces from TIRF microscopy photobleaching movies. I contributed to the project as part of my time working with the lab, building on top of the existing codebase. The lab uses single-molecule photobleaching to count how many fluorophores are attached to a protein of interest. When you image a labeled molecule under TIRF illumination, the fluorophores bleach one at a time, each causing a discrete drop in intensity. Counting those steps tells you the stoichiometry. GLIMPSE automates the pipeline from raw .tif movie to quantified step statistics.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/GLIMPSE.png" alt="GLIMPSE particle detection view" style="max-width: 680px; width: 100%;">
</div>

The pipeline walks through six tabs sequentially. First, the movie is loaded and imaging parameters are set. Then particle detection runs: GLIMPSE identifies fluorophore locations by thresholding and circles them on the frame. The main thing to watch here is particle density. If fluorophores are too crowded, their intensity signals bleed into each other and corrupt the traces.

Cluster removal excludes any fluorophores within a minimum radius of a neighbor. After that, sample sorting filters out particles that never photobleach at all. Non-bleaching particles have to go because they inflate measurements like mean lifetime and survival probability. GLIMPSE generates a pie chart breakdown of viable, edge, clustered, and non-bleaching particles so you can see what is being discarded.

Background correction uses a local approach: for each particle, pixels are sampled from an annular region surrounding it and the median is used as that particle's individual background value. This is more accurate than a single global correction because TIRF images have uneven illumination across the field of view, particularly toward the edges.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/GLIMPSE_trace.png" alt="Single-particle intensity trace showing one photobleaching step" style="max-width: 680px; width: 100%;">
</div>

The trace above shows what a clean single-step photobleach looks like: steady intensity for about 70 seconds, then a sharp drop to background when the fluorophore bleaches. Analysis runs in two rounds. The first applies change-point detection to each trace and outputs molecular brightness, step-wise intensity distributions, and step count histograms. The second round uses a hierarchical clustering approach combining histograms, Gaussian Mixture Models, and distance metrics to resolve noisier recordings or molecules with many closely spaced steps. It also outputs lifetime (τ) and survival probability (q).

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/GLIMPSE_analysis.png" alt="GLIMPSE analysis output with molecular brightness and step histograms" style="max-width: 680px; width: 100%;">
</div>

[View on GitHub](https://github.com/LabGradinaru/GLIMPSE)
