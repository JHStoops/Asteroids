<template>
  <div id="app">
     <h1>Asteroids</h1>
     <div id="canvas" v-on:mousemove="updateXY" v-on:click="shoot">
        <img id="spaceship" v-bind:src="spaceship.img" :style="spaceshipAngle" />
        <div v-for="lazer of lazers" v-model="lazers" v-bind:id="lazer.id" v-bind:style="{ left: lazer.x + 'px', top: lazer.y + 'px'}"></div>
     </div>
  </div>
</template>

<script>
class Lazer {
   constructor(id, x, y, mouseX, mouseY){
      this.id = 'lazer' + id;
      this.x = x;
      this.y = y;

      //Calculate velocity
      var hypotenuse = Math.sqrt((x - mouseX)**2 + (y - mouseY)**2);
      this.velocityX = (mouseX - x) / hypotenuse;
      this.velocityY = (mouseY - y) / hypotenuse;

      let intervalID = setInterval(() => {
         this.x += this.velocityX;
         this.y += this.velocityY;
         console.log(this.x);
         if (this.x > 600 || this.x < 0 || this.y > 600 || this.y < 0) {
            clearInterval(intervalID);
            document.getElementById(this.id).remove();
         }
      }, 1);

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
  data() {
    return {
      spaceship: {
         x: 300.0,
         y: 300.0,
         img: 'src/img/spaceship.png',
         angle: 0
      },
      lazers: [],
      asteroids: [],
      IDCounter: 0
    }
   },
   methods: {
      updateXY: function(e){
         this.spaceship.angle =
            (Math.atan2((this.spaceship.y - e.offsetY), (this.spaceship.x - e.offsetX)) * 180 / Math.PI) - 90;
      },
      shoot: function(e){
         var l = new Lazer(this.IDCounter++, this.spaceship.x, this.spaceship.y, e.offsetX, e.offsetY);
         l.display();
         this.lazers.push(l);
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
      position: relative;
      min-width: 600px;
      min-height: 600px;
      max-width: 600px;
      max-height: 600px;
      background-color: #000000;
      color: #ffffff;
      padding: 0
   }
   #spaceship {
      position: absolute;
      width: 20px;
      height: 32px;
      left: 300px;
      top: 300px;
   }
   [id^='lazer'] {
      position: absolute;
      background-color: #ffffff;
      width: 10px;
      height: 10px;
   }
</style>
