---
layout: page
title: MrLin 2.0
description: Multi-API physics homework solver orchestrating ChatGPT and Wolfram Alpha
img: assets/img/MrLin2.png
importance: 6
category: projects
related_publications: false
---

Named after our high school physics teacher, MrLin 2.0 was a group project built with the same ELROSTEM crew behind Robo AutoScript. It is a Streamlit chatbot that solves physics word problems step by step. The core idea was that ChatGPT is good at understanding natural language and breaking problems into steps, but bad at computing the actual math reliably. Wolfram Alpha is the opposite: terrible at reading a problem, but exact at computation. So we used them together.

The pipeline for each problem: ask ChatGPT what quantity we are solving for in step one, then ask it to extract and format the relevant variables from the problem text. Pass the formatted variables to Wolfram Alpha to compute the answer. Feed that answer back into the conversation and ask ChatGPT whether there are more steps. Repeat until done.

The messiest part was getting Wolfram Alpha to accept the input. ChatGPT does not always phrase variable names in a way Wolfram understands, so there is a retry loop that asks ChatGPT to rephrase the query and tries again before falling back to letting ChatGPT solve it directly.

This was built before the ChatGPT API existed. Accessing GPT required `revChatGPT`, a library that drove a headless Chrome browser to scrape the ChatGPT web interface using Selenium. It worked, but it was fragile: any session timeout or UI change from OpenAI would break it. The whole thing became much cleaner once the API launched, but version 0 running through chromedriver was how it started.

Shortly after we finished, OpenAI released a Wolfram Alpha custom GPT that did essentially the same thing — combining language understanding from ChatGPT with exact computation from Wolfram Alpha. Our effort was not exactly in vain, but the timing was not great.
