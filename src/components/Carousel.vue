<template>
  <div>
    <div class="arrow-left arrow" @click="arrowLeft()"></div>
      <Slide :image="images[currentSlide]"/>
    <div class="arrow-right arrow" @click="arrowRight()"></div>
      <div class="navigation">
        <div 
          v-for="image in images" 
          :key="image.id" 
          @click="handleNavigation(image.id)" 
        >
          <img :src="image.src" style="width: 30px; height: 30px">
        </div>
     </div>
  </div>
</template>
<script>

import Slide from './Slide.vue'

export default {
  name: 'Carousel',
  components: {
    Slide
  },
  data() {
    return {
      images: [
        {
          id: 0,
          src: require('@/assets/slide1.jpg')
        },
        {
          id: 1,
          src: require('@/assets/slide2.jpg')
        },
        {
          id: 2,
          src: require('@/assets/slide3.jpg')
        } 
      ],
      currentSlide: 0,
      intervalObject: null
    }
  },
  methods:{
    handleNavigation(id) {
      this.currentSlide = id
      clearInterval(this.intervalObject)
      this.intervalObject = setInterval(() => {
          this.moveRight();
      }, 4000)
    },

    changeSlide() {
      let counter = this.currentSlide
      counter++
      if (counter >= this.images.length) {
        counter = 0
      }
      this.currentSlide = counter
    },

    arrowLeft() {
      clearInterval(this.intervalObject)
      this.moveLeft()
      this.intervalObject = setInterval(() => {
        this.moveLeft()
      }, 4000)
    },

    arrowRight() {
      clearInterval(this.intervalObject);
      this.moveRight()
      this.intervalObject = setInterval(() => {
        this.moveRight()
      }, 4000)
    },

    moveLeft() {
      let counter = this.currentSlide
      counter++
      if (counter >= this.images.length) {
        counter = 0
      }
      this.currentSlide = counter
    },

    moveRight() {
      let counter = this.currentSlide
      counter--
      if (counter < 0) {
        counter = this.images.length - 1
      }
      this.currentSlide = counter
    }
  },

  created() {
    this.intervalObject = setInterval( () => {
      this.moveLeft()
    }, 3000)
  }
}
</script>
<style lang="scss" scoped>

.arrow {
  cursor: pointer;
  width: 3em;
  height: 3em;
  border-color: #fff;
  position: absolute;
  top: 50%;
  margin-top: -2em;
 
  &.arrow-left {
    border-bottom: .4em solid white;
    border-left: .4em solid white;
    transform: rotate(45deg);
    left: 2em;
    &:active {
      transform: rotate(45deg) scale(1.1);
    }
  }

  &.arrow-right {
    border-bottom: .4em solid white;
    border-left: .4em solid white;
    transform: rotate(-135deg);
    right: 2em;
    &:active {
      transform: rotate(225deg) scale(1.1);
    }
  }
}

.navigation {
  position: absolute;
  bottom: 0;
  left: calc( 50% - 55px);
  background: transparent;
  padding: .5em 2em;
}

 .navigation div {
  margin-right: 10px;
  display: inline-block;
  border-radius:50%;
}
</style>
