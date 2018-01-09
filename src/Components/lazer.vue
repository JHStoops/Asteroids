<template>
	<div id="lazer"></div>
</template>

<script>
export default {
	data() {
		return {
			x: 0,
         y: 0,
         velocityX: 0,
         velocityY: 0
		}
	},
	methods: {
      moveLazers: function(){
         this.x += this.velocityX;
         this.y += this.velocityY;
      },
      renderLazers: function(){
         //What's the best way to render these?

      },
      display(){
         console.log('this.x = ' + this.x);
         console.log('this.y = ' + this.y);
         console.log('this.velocityX = ' + this.velocityX);
         console.log('this.velocityY = ' + this.velocityY);
      },
      destroy: function(){
         //Destroy when it reaches the edge of the map.

      }
	},
	computed: {

	}
}
</script>

<style>
   #lazer {
      background-color: #ffffff;
      width: 10px;
      height: 10px;
   }
</style>
