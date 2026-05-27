---
layout: page
title: Costudify
description: Study session finder that parses ICS calendars to match students with overlapping free time (DeltaHacks)
img: assets/img/DeltaHacks.png
importance: 3
category: mini projects
related_publications: false
---

Built at DeltaHacks, Costudify solves a simple but annoying problem: finding a time when a group of students are all free to study together. You upload your `.ics` calendar file (the standard export format from most university scheduling systems), register an account, and the app parses your schedule and stores it. The schedule view then shows your own classes alongside color-coded availability blocks that reflect how many other registered students are free at each time slot.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/DeltaHacks.png" alt="Costudify weekly schedule view showing classes and shared availability" style="max-width: 680px; width: 100%;">
</div>

The backend is Flask with CSV-based storage. ICS files are parsed using the `icalendar` library, which extracts course codes, days, and time blocks and flattens them into a shared schedule table. The availability view is computed by inverting each student's busy blocks across the week and then finding intersections, so green slots on the grid represent times where the most people are simultaneously free.

[View on GitHub](https://github.com/daniel-halpern/deltahacks-test)
