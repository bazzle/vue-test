<template>
  <div id="app">
    <greeting />
      <div v-if="this.confirmed === false">
        <ul>
          <li v-for="ting in tings" :key="ting">{{ting}}</li>
        </ul>
        <p v-if="tings.length < 1" >No tings in here</p>
        <button v-if="this.state === 'default'" @click="editTings('edit')" class="button">Add some tings</button><br/>
        <div v-if="this.state === 'edit'" class="addTings">
          <input v-model="newTing" type="text" :placeholder="inputPlaceholder" v-on:keyup.enter="addToList" /><br>
          <div v-if="this.newTing.length > 0" class="ting-stuff">
            <a class="button" :href="'https://www.google.com/search?q=' + newTing" target="_blank">Search ting</a>
            <button class="button" v-on:click="addToList">Add to Tings</button>
            <button v-if="this.state === 'edit'" @click="editTings('default')" class="button button--alt">Naaaahh man</button>
          </div>
        </div>
        <button class="button" v-on:click="removeFromList">Remove all tings</button><br/>
        <button class="button button--alt" v-on:click="send">Send tings</button>
      </div>
      <div class="sent" v-if="this.confirmed">
        <p v-if="this.confirmed">Tings are sent, coming to man</p>
        <button @click="restart">Send more tings</button>
      </div>
  </div>
</template>

<script>
import greeting from './components/greeting.vue'

export default {
  name: 'app',
  components: {
    greeting
  },
  data: function () {
    return {
      tings: [],
      inputPlaceholder: 'Someting',
      newTing: '',
      state: 'default',
      confirmed: false
    }
  },
  methods: {
    editTings (arg) {
      this.state = arg
      this.newTing = ''
    },
    addToList () {
      this.tings.push(this.newTing)
      this.newTing = ''
    },
    removeFromList () {
      this.tings = []
    },
    send () {
      this.confirmed = true
    },
    restart () {
      this.confirmed = false
      this.tings = []
    }
  }
}
</script>

<style lang="scss">
body{
  color: white;
  background-color:black;
}
.button{
  border-radius:0;
  background:transparent;
  color:white;
  margin:.2em;
  padding:1em;
  border:1px solid white;
  display:inline-block;
  font-size:1em;
  line-height:1em;
  text-decoration:none;
  &--invert{
    background:white;
    color:black;
  }
  &--alt{
    background:gold;
    color:black;
  }
}
button, input{
  margin:.2em;
  padding:1em;
}
h1, h2, h3, h4, h5{
  text-align:center;
  display:block;
  color:gold;
}
p, ul{
  text-align:center;
  margin:0 auto;
  padding:0;
  margin-bottom:1em;
}
ul{
  list-style-type: none;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 200px;
}
</style>
