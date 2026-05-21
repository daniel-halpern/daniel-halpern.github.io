---
layout: page
title: Shoreline Wave Analysis
description: Computer vision pipeline for quantifying wave dynamics in a physical wave tank
img: assets/img/shoreline_wave_analysis.png
importance: 2
category: research
related_publications: false
---

This is part of the NSF Urban Shorelines Reconfiguration project, which studies seawall designs for NYC coastlines. The core question: can Triply Periodic Minimal Surfaces (TPMS), which are geometries that divide space with minimal surface area, dissipate wave energy better than conventional seawalls? To test that, we needed three things: physical seawall prototypes to test, a wave tank to test them in, and a way to actually measure what the waves were doing.

**TPMS design.** One part of the team worked on parameterizing and 3D printing TPMS structures with varying porosity and geometry. The idea is that the complex surface topology of TPMS should scatter and absorb wave energy more efficiently than a flat or stepped seawall, while also using less material. The goal of the broader project is to iterate on these parameters and find what geometry performs best.

**Wave tank and hardware control.** We built a six-foot acrylic wave tank with a stepper-motor-driven paddle to generate waves at specific frequencies. The motor control runs through an Arduino Nano 33 BLE, and the rest of the team wrote firmware and a Python BLE controller so the wave generator can be adjusted from the same laptop running analysis without touching the tank. There is also a serial fallback and a physical limit-switch mode for when you just want to run the tank standalone.

**Computer vision pipeline.** This was my main contribution. A camera is mounted parallel to the tank cross-section and shoots against a high-contrast background so the water-air interface is visible. From each frame, we apply HSV color-space thresholding to isolate the water, then run edge detection to find the wave boundary. We fit a polynomial curve to that boundary and track it across frames to extract amplitude, period, wavelength, and velocity.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/shoreline_wave_analysis.png" alt="Wave tank camera setup" style="max-width: 640px; width: 100%;">
</div>

Velocity was the trickiest metric. Amplitude you can read off a single frame, but velocity requires tracking the wave front across time, which means dealing with noise between frames and deciding how to correlate the same wave crest across multiple detections. I also added centimeter calibration to the GUI so the pixel measurements map to physical units, and graph export so results can go straight into lab reports.

Everything ties together in a MATLAB App Designer GUI. The person running an experiment can set wave frequencies, import a video, run the analysis, and export graphs without touching any code. We also ran a session at the ERHS STEM Workshop where students designed their own seawall prototypes and used the pipeline to measure how well each design dissipated wave energy compared to the TPMS models.

[View on GitHub](https://github.com/ELROSTEM/shoreline-wave-analysis)
