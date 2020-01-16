<template>
  <div class="addTings">
    <button v-if="this.state === 'default'" @click="editTings('edit')" class="button">Add some tings</button>
    <div v-if="this.state === 'edit'" class="addTings__inner">
        <div class="row row--mb">
            <input ref="inputTing" class="addTings__input" v-model="newTing" type="text" :placeholder="inputPlaceholder" :maxlength="inputCharacterMax" />
            <div class="addTings__character-count"><span>{{newTing.length}} / {{inputCharacterMax}}</span></div>
        </div>
        <div :class="{'addTings__controls--disabled' : newTing.length < 1 }" class="row addTings__controls">
          <button v-on:click="cancelTing" class="button addTings__controls__cancel">Cancel</button>
          <a class="button" disabled="true" :href="'https://www.google.com/search?q=' + newTing" target="_blank" title="Search ting name on google">Search ting</a>
          <button class="button button--alt-invert" v-on:click="addtoTings">Add to Tings</button>
        </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'addTing',
  data: function () {
    return {
      newTing: '',
      state: 'default',
      inputCharacterMax: 20,
      inputPlaceholder: 'Someting'
    }
  },
  methods: {
    addtoTings () {
      this.$parent.tings.push({
        name: this.newTing,
        sent: false,
        stock: 1
      })
      this.newTing = ''
    },
    cancelTing () {
      this.state = 'default'
    },
    editTings (arg) {
      this.state = arg
      this.newTing = ''
    }
  }
}
</script>
<style lang="scss">

</style>
