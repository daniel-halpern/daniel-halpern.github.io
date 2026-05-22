---
layout: page
title: Food Allergy Detector
description: Transfer learning food classifier with a local LLM for allergen safety assessment
img: assets/img/FoodAllergyDetector.png
importance: 7
category: projects
related_publications: false
---

Built for my Robotics and AI class at the end of senior year, this Streamlit app takes a photo of food and tells you whether it is safe to eat given your allergies. The pipeline has two stages: a CNN classifies what food is in the image, then a local LLM evaluates whether that food is safe for your specific allergies.

<div style="text-align: center; margin-top: 1.5rem; margin-bottom: 1.5rem;">
  <iframe width="640" height="360" src="https://www.youtube.com/embed/KPGQxvGKgfM" title="Food Allergy Detector Demo" frameborder="0" allowfullscreen style="max-width: 100%;"></iframe>
</div>

The classifier is VGG16 fine-tuned on a food dataset using transfer learning. It returns the top predictions and lets the user confirm or override if the model is wrong. Once the food is confirmed, the user selects their allergies from a list and the app passes a prompt to a locally running Llama 3 instance via Ollama, asking whether the average preparation of that food contains the specified allergens. Keeping the LLM local meant no API costs and no data leaving the machine.

[View on GitHub](https://github.com/daniel-halpern/FoodAllergyDetector)
