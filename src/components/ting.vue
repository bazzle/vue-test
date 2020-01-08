<template>
  <li class="ting">{{ting.name}}</li>
</template>
<script>
export default {
  name: 'Ting',
  props: {
    name: String,
    ordered: Boolean,
    stock: Number
  }
}
</script>
<style lang="scss">

</style>
