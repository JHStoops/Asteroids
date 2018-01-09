<template>
  <div id="app">
     <h1>Asteroids</h1>
     <div id="canvas" v-on:mousemove="updateXY" v-on:click="shoot">
        <img id="spaceship" v-bind:src="spaceship.img" :style="spaceshipAngle" />
     </div>
  </div>
</template>

<script>
import lazer from './Components/lazer.vue';

class Lazer {
   constructor(x, y, mouseX, mouseY){
      this.x = x;
      this.y = y;

      //Calculate velocity
      var hypotenuse = Math.sqrt((x - mouseX)**2 + (y - mouseY)**2);
      this.velocityX = (mouseX - x) / hypotenuse;
      this.velocityY = (mouseY - y) / hypotenuse;

      //Create DOM element

   }

   display(){
      console.log('this.x = ' + this.x);
      console.log('this.y = ' + this.y);
      console.log('this.velocityX = ' + this.velocityX);
      console.log('this.velocityY = ' + this.velocityY);
   }

   destroy(){
      //Remove DOM element
   }
}

export default {
  name: 'app',
  components: {
     'lazer': lazer
  },
  data () {
    return {
      spaceship: {
         x: 300,
         y: 300,
         img: 'src/img/spaceship.png',
         angle: 0
      },
      lazers: [],
      asteroids: []
    }
   },
   methods: {
      updateXY: function(e){
         this.spaceship.angle =
            (Math.atan2((this.spaceship.y - e.offsetY), (this.spaceship.x - e.offsetX)) * 180 / Math.PI) - 90;
      },
      shoot: function(e){
         var l = new Lazer(this.spaceship.x, this.spaceship.y, e.offsetX, e.offsetY);
         l.display();
         this.lazers.push(l);
         console.log(this.lazers.length)
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
