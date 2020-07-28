<template>
  <div class="v-carousel-item">
    <img :width="slideSize.width" :height="slideSize.height"
         v-if="imageSlide"
         class="v-carousel-item__img"
         :src="require('../assets/images/' + item_data.img)"
         alt="img">
    <div class="item__content" v-else>
      <div>{{item_data.name}}</div>
      <div>{{item_data.id}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'v-carousel-item',
  props: {
    item_data: {
      type: Object,
      default() {
        return {}
      }
    },
    imageSlide: {
      type: Boolean,
      default: true
    },
     slideSize: {
      type: Object,
      required: true
    }
  },
}
</script>

<style lang="scss">
  .v-carousel-item {

    &__img {
      display: block;
      object-fit: cover;
    }

  }
</style>
