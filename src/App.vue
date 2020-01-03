<template>
  <div id="app">
    <greeting />
    <hr class="divider" />
      <div v-if="this.confirmed === false">
        <ul>
          <li v-for="ting in tings" :key="ting" class="ting" :class="[ting.ordered ? 'ordered' : '', ting.stock === 0 ? 'unavailable' : '']">
            {{ting.name}} <span class="stock-level"> – {{ ting.stock === 0 ? 'Out of stock' : 'In stock' }}</span>
          </li>
        </ul>
        <p v-if="tings.length < 1" >No tings in here</p>
        <button v-if="this.state === 'default'" @click="editTings('edit')" class="button">Add some tings</button>
        <div v-if="this.state === 'edit'" class="addTings">
          <div class="row">
            <input class="addTings__input" v-model="newTing" type="text" :placeholder="inputPlaceholder" />
          </div>
          <div class="row">
            <a class="button" :href="'https://www.google.com/search?q=' + newTing" target="_blank" title="Search ting name on google">Search ting</a>
            <button class="button" v-on:click="addtoTings">Add to Tings</button>
            <button v-if="this.state === 'edit'" @click="editTings('default')" class="button">Cancel</button>
          </div>
        </div>
        <hr class="divider" />
        <div class="row">
          <button class="button" v-on:click="removeFromList">Remove all tings</button>
          <button class="button button--alt" v-on:click="send">Send tings</button>
        </div>
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
      tings: [
        {
          name: 'Reebok Classic',
          ordered: false,
          stock: 2
        },
        {
          name: 'Adidas Originals',
          ordered: false,
          stock: 1
        },
        {
          name: 'Vans Old School',
          ordered: false,
          stock: 2
        }
      ],
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
    addtoTings () {
      this.tings.push({
        name: this.newTing,
        sent: false
      })
      this.newTing = ''
    },
    removeFromList () {
      this.tings = []
    },
    send () {
      this.tings.forEach(ting => {
        ting.stock = ting.stock - 1
      })
      this.confirmed = true
    },
    restart () {
      this.confirmed = false
    }
  }
}
</script>

<style lang="scss">
h1, h2, h3, h4, h5{
  margin:0;
  padding:0;
}
html, body{
  width:100%;
  height:100%;
}
body{
  color: white;
  background-color:black;
  display:flex;
  align-items:center;
  justify-content:center;
}
.row{
  display:flex;
  justify-content:space-between;
  & *{
    flex-grow:1;
  }
}
.button{
  border-radius:0;
  background:black;
  color:white;
  margin:.2em;
  padding:1em;
  border-radius:5px;
  font-size:1em;
  line-height:1em;
  text-decoration:none;
  border:none;
  cursor:pointer;
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
  max-width:600px;
  background-color:rgba(white, .1);
  padding:2em;
  border-radius: .5em;
}
.addTings{
  .button{
    font-size:.7em;
    font-weight:700;
  }
  &__input{
    width:100%;
  }
}
.divider{
  background-color:black;
  height:1px;
  border: none;
  border-bottom: 1px solid rgba(white, .17);
  margin-top:1em;
  margin-bottom:1em;
}
.unavailable{
  text-decoration: line-through;
  color:rgba(white, .2)
}
.ordered{
  color:green;
}
</style>
