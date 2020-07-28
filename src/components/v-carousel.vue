<template>
  <div class="wrapper" :style="slideSize">
    <div class="v-carousel" :style="{transform: translateX}"
         :class="{'v-carousel__hasTransition': hasTransition}">
      <v-carousel-item v-for="item of carousel_data"
                      :key="item.id"
                      :item_data="item"
                      :slideSize="slideSize"
      />
    </div>
    <button class="v-carousel__btn v-carousel__btn-prev"
            value="prev"
            @click="changeSlide"
    >Prev
    </button>
    <button class="v-carousel__btn v-carousel__btn-next"
            value="next"
            @click="changeSlide"
    >Next
    </button>
  </div>
</template>

<script>
import  vCarouselItem from './v-carousel-item'

export default {
  name: 'vCarousel',
  components: {
    vCarouselItem
  },
  props: {
    carousel_data: {
      type: Array,
      default() {
        return []
      }
    },
    interval: {
      type: Number,
      default: 0
    },
    slideSize: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      currentSlideIndex: 0,
      hasTransition: true,
      change: null
    }
  },
  mounted() {
    if (this.interval > 0) {
      setInterval(() => {this.nextSlide()}, this.interval)
    }
    this.change = this.debounce(this.sliderHandler)
  },
  computed: {
    translateX() {
      return `translateX(${-this.currentSlideIndex * 100}%)`
    }
  },
  methods: {
    changeSlide({target}) {
      this.change(target.value);
    },
    sliderHandler(direction) {
      let shiftSliderIndex
      if (direction === 'next') shiftSliderIndex = 1
      else if (direction === 'prev') shiftSliderIndex = -1

      if(direction === 'prev' && this.currentSlideIndex > 0) this.currentSlideIndex += shiftSliderIndex
      else if (direction === 'next' && this.currentSlideIndex < this.carousel_data.length - 1) this.currentSlideIndex += shiftSliderIndex
      else {
        this.hasTransition = false
        this.$emit('slide:change', direction)
        this.currentSlideIndex -= shiftSliderIndex
        setTimeout(()=> {
          this.hasTransition = true
          this.currentSlideIndex += shiftSliderIndex
        }, 0)
      }
    },
    debounce(callback) {
      const DEBOUNCE_DURATION = 50;
      let timeout;
      return (arg) => {
        clearTimeout(timeout);
        timeout = setTimeout(callback, DEBOUNCE_DURATION, arg);
      };
    }
  }
}
</script>

<style lang="scss">
  .wrapper {
    position: relative;
    overflow: hidden;
    padding: 0 0 40px;
    margin: 20px auto;
  }

  .v-carousel {
    display: flex;

    &__hasTransition {
      transition: transform ease .5s;
    }

    &__btn {
      position: absolute;
      bottom: 0;
      left: 50%;
      padding: 5px 10px;

      &-prev {
        transform: translateX(-110%)
      }

      &-next {
        transform: translateX(10%)
      }

    }

  }

</style>
