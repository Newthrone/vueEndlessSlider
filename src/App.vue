<template>
  <div id="app">
    <v-carousel :carousel_data="sliderItems"
                :slideSize="slideSize"
                @slide:change="reconfigurationSlider"
    />
  </div>
</template>

<script>
import vCarousel from './components/v-carousel'

export default {
  name: 'App',
  components: {
    vCarousel
  },
  data() {
    return {
      sliderItems: [
        { id: 1, name: 'img1', img: '1.jpg'},
        { id: 2, name: 'img2', img: '2.jpg'},
        { id: 3, name: 'img3', img: '3.jpg'},
        { id: 4, name: 'img4', img: '4.jpg'},
        { id: 5, name: 'img5', img: '5.jpg'},
        { id: 6, name: 'img6', img: '6.jpg'}
      ],
      slideSize: {
        width: '300px',
        height: '200px'
      }
    }
  },
  methods: {
    reconfigurationSlider(direction) {
      if (direction === 'next') this.sliderItems.push(this.sliderItems.shift())
      else if (direction === 'prev') this.sliderItems.unshift(this.sliderItems.pop())
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
