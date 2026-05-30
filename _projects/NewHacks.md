---
layout: page
title: Rescue Radar
description: Real-time disaster reporting platform with Bayesian inference on resource availability (NewHacks 2024)
img: assets/img/NewHacks.png
importance: 2
category: mini projects
related_publications: false
---

Built at NewHacks 2024, Rescue Radar is a disaster reporting platform where people on the ground can file live condition reports during a natural disaster. You drop a pin on the map, fill out a form covering disaster type, severity, casualties, and whether the area has shelter, food, water, and electricity, and the report gets logged. The map view aggregates all incoming reports so responders can see where conditions are worst at a glance.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/NewHacks.png" alt="Rescue Radar live condition report form with map" style="max-width: 680px; width: 100%;">
</div>

The backend is Flask with CSV storage. The more interesting piece is the analytics layer, which uses a Bayesian network built with `pgmpy` to model conditional dependencies between reported conditions. The idea is that knowing a house is structurally intact shifts the probability estimates on whether shelter is available nearby. K-means clustering groups reports by geographic proximity so the insights page can surface which areas need the most coordinated response.

[View on GitHub](https://github.com/pwatana/NewHacks-project)
