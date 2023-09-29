---
toc: false
comments: false
layout: post
title: My Animation
description: Trying to animate my own sprite on the basis of the dog animation.
type: hacks
courses: { compsci: {week: 4} }
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
      body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
      }
      #content-container {
        text-align: center;
      }
      canvas {
        display: block;
        margin: 0 auto;
      }
  </style>
</head>
<body>
    <div>
        <canvas id="spriteContainer">
            <img id="catSprite" src="../../../../images/catplayersprite.png">
        </canvas>
        <div id="controls">
          <button id="idleButton">Idle</button>
          <button id="barkingButton">Barking</button>
          <button id="walkingButton">Walking</button>
        </div>
    </div>
</body>
<script>
window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        const SPRITE_WIDTH = 160;
        const SPRITE_HEIGHT = 144;
        const SCALE_FACTOR = 2;
        const FRAME_LIMIT = 48;
        const FRAME_RATE = 15;
        let isWalking = false;
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;
        class Cat {
            constructor() {
                this.image = document.getElementById("catSprite");
                this.spriteWidth = SPRITE_WIDTH;
                this.spriteHeight = SPRITE_HEIGHT;
                this.width = this.spriteWidth;
                this.height = this.spriteHeight;
                this.x = 0;
                this.y = 0;
                this.scale = 1;
                this.minFrame = 0;
                this.maxFrame = FRAME_LIMIT;
                this.frameX = 0;
                this.frameY = 0;
            }
            draw(context) {
                context.clearRect(0, 0, canvas.width, canvas.height); // Clear the canvas
                context.drawImage(
                    this.image,
                    this.frameX * this.spriteWidth,
                    this.frameY * this.spriteHeight,
                    this.spriteWidth,
                    this.spriteHeight,
                    this.x,
                    this.y,
                    this.width * this.scale,
                    this.height * this.scale
                );
            }
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }
        const cat = new Cat();
        const controls = document.getElementById('controls');
        controls.addEventListener('click', function (event) {
            if (event.target.tagName === 'BUTTON') {
                const selectedAnimation = event.target.id;
                switch (selectedAnimation) {
                    case 'idleButton':
                        cat.frameY = 0;
                        isWalking = false;
                        break;
                    case 'barkingButton':
                        cat.frameY = 1;
                        isWalking = false;
                        break;
                    case 'walkingButton':
                        cat.frameY = 2;
                        isWalking = true;
                        break;
                    default:
                        break;
                }
            }
        });
        function animate() {
            cat.update();
            cat.draw(ctx);
            if (isWalking) {
                requestAnimationFrame(animate);
            }
        }
        animate();
});
</script>
</html>
