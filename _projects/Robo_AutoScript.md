---
layout: page
title: Robo AutoScript
description: Natural language to robot code using LLMs and RAG
img: assets/img/RoboAutoScript.png
importance: 3
category: projects
related_publications: false
---

In 2022, four of us at Eleanor Roosevelt High School got curious about whether you could use language models to program robots from plain English. Google had just published SayCan, which showed LLMs being used for robot task planning, and we wanted to try something like that for our VEX robots. We placed 2nd in our congressional district and received a letter from Congresswoman Maloney.

<div style="text-align: center; margin-top: 1.5rem; margin-bottom: 1.5rem;">
  <iframe width="640" height="360" src="https://www.youtube.com/embed/UwRmSTzJoDI" title="Robo AutoScript Demo" frameborder="0" allowfullscreen style="max-width: 100%;"></iframe>
</div>

The app takes a plain English command, typed or spoken, and produces a working RobotC program. Under the hood it runs a two-stage pipeline. A Planner agent breaks the input down into a list of atomic robot actions. A Coder agent turns that list into actual code. Keeping them separate matters because the Planner can catch things the Coder should never have to deal with. If you tell the robot to fly, the Planner removes it from the plan before the Coder ever sees it.

Hardware compatibility took longer to get right than expected. VEX robots come in different drivetrain configurations, so you cannot generate generic code. A 4-motor drivetrain needs all four motors addressed in the output, or the robot drifts. We handled this by having users paste their motor boilerplate into the app as context, then giving the Coder an explicit constraint: whatever motors appear in the boilerplate have to appear in the output.

For grounding the generated code against the actual RobotC API, we built a small RAG pipeline. The robot hardware manual is chunked into 400-token segments, indexed in a FAISS vector store, and the top 2 most relevant chunks for each action get retrieved at generation time. The retrieval is per action rather than per query, so the code for moving the arm gets the arm documentation, not the drive documentation.

The most annoying problem was the RobotC compiler itself. RobotC only runs as a Windows GUI app with no command-line interface, so there was no clean way to automate it. We ended up using PyAutoGUI to script mouse clicks through the File menu to trigger compilation. Not pretty, but it worked.

[View on GitHub](https://github.com/ELROSTEM/Robo-autoscript)
