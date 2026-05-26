---
layout: page
title: Angry Birds
description: Physics-based Angry Birds clone built with Pygame and Pymunk rigid body dynamics
img: assets/img/AngryBirds.png
importance: 1
category: games
related_publications: false
---

After the AP Physics exam, our class had open time to build whatever we wanted as long as it involved physics. I decided to program Angry Birds.

<div style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/img/AngryBirds.png" alt="Angry Birds clone gameplay" style="max-width: 640px; width: 100%;">
</div>

My first instinct was to write the physics myself since that was kind of the point. I got projectile motion working fine, and it was actually satisfying to implement things like angular velocity and angular momentum for real. The problem was rotation. When a block gets hit and starts tumbling, you have to track its angle, update it every frame based on angular velocity, and redraw it correctly. Rotating rectangles in Pygame is a mess because you have to re-derive the bounding box every frame to avoid clipping artifacts, and bugs in the rotation logic made the blocks behave in increasingly unhinged ways.

Eventually I gave up on the homebrew physics and switched to Pymunk, a Python wrapper around the Chipmunk 2D physics engine. Once that was in, everything that had been painful, block collisions, the slingshot launch arc, pigs taking damage on impact, came together quickly. The lesson was less about physics and more about knowing when to stop reinventing the wheel.

[View on GitHub](https://github.com/daniel-halpern/AngryBirds)
