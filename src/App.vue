<template>
  <div id="app">
    <greeting msg = "Hi fam" />
    <hr class="divider" />
      <div v-if="this.confirmed === false">
        <ul>
          <ting v-for="ting in reversedList" :key="ting.key" :name="ting.name" :ordered="ting.ordered" :stock="ting.stock" />
        </ul>
        <p v-if="this.tings.length < 1" >No tings in here</p>
        <!-- Input section -->
        <addTing />
        <!-- End input section -->
        <hr class="divider" />
        <div v-if="this.tings.length > 0" class="row">
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
import ting from './components/ting.vue'
import addTing from './components/addTing.vue'

export default {
  name: 'app',
  components: {
    greeting,
    ting,
    addTing
  },
  data: function () {
    return {
      tings: [
        {
          name: 'Reebok Classic',
          stock: 2
        },
        {
          name: 'Adidas Originals',
          stock: 1
        },
        {
          name: 'Vans Old School',
          stock: 2
        }
      ],
      confirmed: false
    }
  },
  methods: {
    removeFromList () {
      this.tings = []
    },
    send () {
      this.tings.forEach(ting => {
        if (ting.stock > 0) {
          ting.stock = ting.stock - 1
        }
      })
      this.confirmed = true
    },
    restart () {
      this.confirmed = false
    }
  },
  computed: {
    reversedList () {
      return this.tings.slice(0).reverse()
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
  &--mb{
    margin-bottom:1em;
  }
}
.disabled{
  color:rgba(black,.5);
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
  &--alt-invert{
    color:gold;
    background:black;
  }
}
button, input{
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
.stock-level{
  &__number{
    font-size:.8em;
  }
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  max-width:300px;
  background-color:rgba(white, .1);
  padding:2em;
  border-radius: .5em;
  width:100%;
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
</style>
