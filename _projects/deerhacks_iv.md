---
layout: page
title: Real-Playing Game
description: Campus exploration RPG with GPS path tracking and AI-powered location verification
img: assets/img/deerhacks_iv.png
importance: 1
category: mini projects
related_publications: false
---

Built at DeerHacks IV, Real-Playing Game (RPG) is a campus exploration app for UTM. The premise is simple: most of us had been at the university for over a semester and still barely knew the campus. The app tracks where you have physically walked, colors your explored paths on the map, and shows you what you have not seen yet. It also serves location-based tasks, pushing you toward spots you would not normally visit.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/deerhacks_iv.png" alt="RPG campus map showing explored and unexplored paths" style="max-width: 640px; width: 100%;">
</div>

The map shows explored paths in green and unvisited routes in red, and calculates the percentage of campus you have covered. There is a leaderboard so you can compare progress with friends. For location tasks, completion is verified through Gemini: you take a photo at the location and the model confirms you actually went there rather than just walking nearby.

The stack is React on the frontend, Flask on the backend, and Leaflet.js with MapTiler for the mapping layer. The trickiest part was the path calculation system since MapTiler's documentation for road and path network data was harder to work with than expected.

[View on GitHub](https://github.com/daniel-halpern/deerhacks-iv)
