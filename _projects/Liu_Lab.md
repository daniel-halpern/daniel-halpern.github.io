---
layout: page
title: Liu Lab
description: Real-time behavioral neuroscience rig controller for mouse visual discrimination experiments
img: assets/img/Liu_Lab.png
importance: 3
category: research
related_publications: false
---

<div style="border-left: 4px solid #f0ad4e; background: #fff8f0; padding: 0.8rem 1.2rem; margin-bottom: 1.5rem; border-radius: 0 4px 4px 0;">
  <strong>Work in progress.</strong> This is ongoing research from Summer 2026. This page will be updated as the work continues.
</div>

I work on the software for the Liu Lab that runs visual discrimination experiments on mice, contributing to an existing codebase. The experiment is a Go/No-Go task: the mouse sits on a running wheel and watches a screen. When a Gabor patch (a sinusoidal grating inside a Gaussian envelope, like the image below) appears at a particular orientation, the mouse is trained to lick a spout to receive a water reward. A different orientation is the No-Go stimulus, where licking is not rewarded. By varying the stimuli, the lab can probe the mouse's perceptual thresholds and how neural circuits encode visual information.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/Liu_Lab.png" alt="Gabor patch stimulus used in the visual discrimination task" style="max-width: 580px; width: 100%;">
</div>

The controller is a MATLAB finite state machine (FSM) that coordinates everything: generating pseudorandomized trial sequences, rendering stimuli frame-by-frame via Psychtoolbox, communicating with the hardware, logging behavioral data, and updating live plots on the GUI. The randomization is constrained so the mouse cannot be dealt too many consecutive trials of the same type, which would let it develop a bias without actually discriminating.

The hardware side runs on a Teensy Arduino, which handles the real-time tasks MATLAB cannot reliably do at millisecond precision: reading the rotary encoder for running speed, detecting licks, and triggering the water solenoid on a correct response. MATLAB and the Teensy communicate over serial every frame, so the stimulus machine can react to licks within the trial window and record the outcome (Hit, Miss, False Alarm, or Correct Rejection).

The stimulus rendering runs on a secondary monitor dedicated to the mouse, with gamma correction applied from a calibration file tuned to the mouse's visual acuity. Gabor textures are pre-generated and loaded into the GPU at startup so they can be drawn without per-frame computation lag.
