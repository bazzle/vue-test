<template>
  <li class="ting" :class="[this.stock < 1 ? 'unavailable' : '']">
    <span class="ting__name">{{this.name}}</span>
    <span class="stock-level"> – {{ this.stock === 0 ? 'Out of stock' : 'In stock' }} <span class="stock-level__number">({{this.stock}})</span></span>
  </li>
</template>
<script>
export default {
  name: 'ting',
  props: {
    name: {
      type: String,
      required: true
    },
    stock: {
      type: Number,
      required: true
    }
  }
}
</script>
<style lang="scss">
  .ting{
    &__name{
      font-weight:bold;
    }
  }
</style>
