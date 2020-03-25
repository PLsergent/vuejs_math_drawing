<template>
  <div id="vue-canvas"></div>
</template>

<script>
export default {
  name: "VueCanvas",
  mounted() {
    const script = function(p5) {
      var speed = 2;
      var posX = 35;
      var angle = 0;
      var x, y, a, b;

      // NOTE: Set up is here
      p5.setup = () => {
        const canvas = p5.createCanvas(1800, 800);
        canvas.parent("vue-canvas");
        canvas.background(245);
        canvas.strokeWeight(4);
        p5.angleMode(p5.DEGREES);
        p5.frameRate(250);
        x = 0;
        y = 0;
        a = 30;
        b = 1;
        console.log(x, y, a, b, angle, speed, posX);
      };
      // NOTE: Draw is here
      p5.draw = () => {
        // draw a sine wave
        p5.stroke("red");
        var dy = 50 * (2 * p5.cos(3*angle) - p5.sin(angle));
        p5.point(x, 200 - dy);

        // increment for next points
        angle += 5;
        x += 5;
        y++;

        // p5.background(245);
        // const degree = p5.frameCount * 3;
        // const y = p5.sin(p5.radians(degree)) * 50;

        // p5.push();
        // p5.translate(0, p5.height / 2);
        // p5.fill(66, 184, 131);
        // p5.stroke(53, 83, 94);
        // p5.strokeWeight(5);
        // p5.ellipse(posX, y, 50, 50);
        // p5.pop();
        // posX += speed;

        // if (posX > p5.width - 35 || posX < 35) {
        //   speed *= -1;
        // }
      };
    };
    // NOTE: Use p5 as an instance mode
    const P5 = require("p5");
    new P5(script);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#vue-canvas {
  display: block;
  margin: 0 auto;
  padding: 0;
  width: 1000px;
  height: 500px;
  border-radius: 20px;
  overflow: hidden;
}
</style>