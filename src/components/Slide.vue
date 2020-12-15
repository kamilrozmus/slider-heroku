<template>
  <transition-group name="fade" mode="out-in" tag="div" id="slide">
    <div class="image" :style="getImage" :key="image.id">
      <div class="image__content">
        <div class="title">
          Spring 2019
        </div>
        <div class="description">
          Lorem ipsum dolor sit amet consectetur adipisicing elit.
        </div>
        <div class="buttons" style="margin-top: 1em;">
          <button>
            Shop Womens
          </button>
          <button>
            Shop Mens
          </button>
        </div>
      </div>
    </div>
  </transition-group>
</template>
<script>
export default {
  name: 'Slide',
  props: {
    image: {
      type: Object
    }
  },
  computed: {
    getImage() {
      return { backgroundImage: "url("+this.image.src+")" }
    }
  }
}
</script>
<style lang="scss" scoped>
.image {
  height: 100vh;
  width: 100%;
  user-select: none; 
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none; 
  -moz-user-select: none; 
  -ms-user-select: none;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  animation-fill-mode: forwards;
  color: white;

  &__content {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    height: 100vh;
  }
}

.fade-move {
  transition: all 1s;
}

.fade-enter-active {
    animation-name: fadeIn;
    animation-duration: 1s;
    animation-iteration-count: 1;
}

.fade-move {
    transition: all 1s;
}

.fade-leave-active {
    animation-name: fadeOut;
    animation-duration: 1s;
    animation-iteration-count: 1;
    position: absolute;
}

@keyframes fadeIn {
    from {
        opacity:0;
    }

    to {
        opacity:1;
    }
}

@keyframes fadeOut {
    from {
        opacity:1;
    }

    to {
        opacity:0;
    }
}

.title {
  text-transform: uppercase;
  font-size: 2em;
  font-weight: 550;
}

.description {
  font-size: .8em;
  margin-top: .8em;
}

button {
  background: transparent;
  color: white;
  text-transform: uppercase;
  border: .2em solid white;
  padding: .6em 3em;
  font-weight: 600;
  margin: 0 2em;
  outline: none;
  cursor: pointer;
  &:focus {
    outline: none;
    box-shadow: none;
  }
  &:hover {
    color: black;
    background: white;
  }
}

@media screen and (max-width: 567px) {
  .image__content {
    margin: 0 2em;
  }

  .buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
    button {
      width: 70%;
      margin: .4em 0;
    }
  }
}
</style>
