---
layout: page
title: BattleTrains
description: Battleship variant with constraint-based random board generation and a two-tier AI opponent
img: assets/img/BattleTrains.png
importance: 2
category: games
related_publications: false
---

BattleTrains is a Battleship clone built in Python with cmu-graphics, with trains instead of ships. Each piece is a multi-car train that can bend and branch across the grid rather than sitting in a straight line, which makes the game feel noticeably different from standard Battleship.

<div style="text-align: center; margin-top: 1.5rem; margin-bottom: 1.5rem;">
  <iframe width="640" height="360" src="https://www.youtube.com/embed/_T4J82Es0Eg" title="BattleTrains Demo" frameborder="0" allowfullscreen style="max-width: 100%;"></iframe>
</div>

The board generation was the most interesting part to get right. Trains are placed procedurally using a constrained random walk: each car extends from the previous one, weighted to keep going in the initial direction but with a chance to turn. After each placement, the board is checked for legality (no overlaps, stays in bounds). If the algorithm gets stuck and cannot place a train within a set number of attempts, it discards the whole board and starts over rather than softlocking.

The AI has two modes. When it has no information it guesses randomly. Once it scores a hit, it switches to a targeted mode and probes the adjacent cells around the hit before going back to random guessing. It also has an artificial delay before each move so it does not feel instant.

[View on GitHub](https://github.com/daniel-halpern/BattleTrains)
