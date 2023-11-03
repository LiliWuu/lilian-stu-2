---
toc: true
comments: true
layout: post
title: Review Ticket 10
description: This is where I will put my questions and feedback and improvements.
type: tangibles
courses: { compsci: {week: 6} }
---

## What I Did
- [Finalized the coyote animation](https://github.com/kaylale124/final-game/commit/563c2c9f005510ef8c312dd8fc15fd0f6573f420)
    - Made them pyramid shaped
    - Can move downwards on screen
- [Made the game screen (where players would actually get to play the game)](https://github.com/kaylale124/final-game/commit/88fc4181fa3d61ca91553741f45163bd23ac0c5f)
    - Tried to integrate coyotes and background together

## Fails
- [Tried putting score in with coyotes and background](https://github.com/kaylale124/final-game/commit/0a792af965592520afa532f326ea31e42028b0d7)
    - Was trying to do different collision detections to decrement score
        - Backgroundbottom, creating a collision object in the md file directly
Solutions:
- Consulted teacher for help
    - Was told to use OOP instead
    - Gave me code to use as a basis
    - [Edited a few file names in the new code](https://github.com/kaylale124/final-game/commit/a41310d9991d41374557bb2d12d8ed76db572556)
    - [Made coyote animation speed slower](https://github.com/kaylale124/final-game/commit/3c58ff9f5b35eea4667e7f4c7ecc408677e3f4ea) (so they would descend slower too)
