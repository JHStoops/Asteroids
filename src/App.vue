<template>
  <div id="app">
     <h1>Asteroids</h1>
     <div id="canvas" v-on:mousemove="updateXY">
        <img id="spaceship" v-bind:src="spaceship.img" :style="spaceshipAngle" />
     </div>
  </div>
</template>

<script>
class Lazer {
   constructor(x, y, mouseX, mouseY){
      this.x = x;
      this.y = y;
      var tangens = Math.atan2((this.y - mouseY), (this.x - mouseX));
      this.velocityX = tangens;
      this.velocityY = 1 - tangens;
   }

   display(){
      console.log('this.x = ' + this.x);
      console.log('this.y = ' + this.y);
      console.log('this.velocityX = ' + this.velocityX);
      console.log('this.velocityY = ' + this.velocityY);
   }
}

export default {
  name: 'app',
  data () {
    return {
      spaceship: {
         x: 300,
         y: 300,
         img: 'src/img/spaceship.png',
         angle: 0
      },
      lazers: [
         //{x: 0, y: 0, velocityX: 0, velocityY: 0}
      ],
      asteroids: []
    }
   },
   methods: {
      updateXY: function(e){
         this.spaceship.angle =
            (Math.atan2((this.spaceship.y - e.offsetY), (this.spaceship.x - e.offsetX)) * 180 / Math.PI) - 90;
      },
      moveLazers: function(){
         this.lazers.map()
      }
   },
   computed: {
      spaceshipAngle(){
       	return {
           'transform':'rotate(' + this.spaceship.angle + 'deg)'
           }
       }
   }
}
</script>

<style>
   #canvas {
      min-width: 600px;
      min-height: 600px;
      max-width: 600px;
      max-height: 600px;
      background-color: #000000;
      color: #ffffff;
      padding: 0
   }
   #spaceship {
      position: relative;
      width: 20px;
      height: 32px;
      left: 300px;
      top: 300px;
   }
</style>
