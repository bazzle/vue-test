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
.addTings{
  .button{
    font-size:.7em;
    font-weight:700;
  }
  &__input{
    width:100%;
    border-radius:5px;
    border:none;
  }
  &__character-count{
    display:flex;
    align-items: center;
    justify-content: center;
    margin-left:.4em;
    padding:0 1em;
    border-radius:5px;
    border:none;
    background-color:rgba(white,.1);
    font-size:.8em;
    white-space: nowrap;
  }
  &__controls{
    &--disabled{
      .button:not(.addTings__controls__cancel){
        opacity:.3;
      }
    }
  }
}
</style>
