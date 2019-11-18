<template>
  <div class="gen">
    <h1>{{ msg }}</h1>
    <h2 v-on:click="gen">{{ randstr }}</h2>
    <div>
      <h3>Settings</h3>
      <br>
      <vue-slide-bar v-model="length" style="width:500px;margin: 0 auto;"/>
       <b>{{length}}</b>
       <div>
         <button class="button" @click="length--">
           -
         </button>
         <button class="button" @click="length++">
           +
         </button>
       </div>
      <input type="checkbox" id="number" value="number" v-model="pattern">
      <label for="number">number</label>
      <input type="checkbox" id="symbol" value="symbol" v-model="pattern">
      <label for="symbol">symbol</label>
      <input type="checkbox" id="upper" value="upper" v-model="pattern">
      <label for="upper">upper case</label>  
    </div>
    <span>length:  {{length}}</span><br>
    <span>Pattern: {{ pattern }}</span>
  </div>
</template>

<script>
import VueSlideBar from 'vue-slide-bar'

export default {
  name: 'Gen',
  props: {
    msg: String
  },
  components:{
    VueSlideBar
  },
  data : function(){ 
     return {
       randstr:"click me!",
       length: 16,
       pattern:[],
       pmap: {
         "lower":RandomFactory('a'.charCodeAt(0),'z'.charCodeAt(0)),
         "upper":RandomFactory('A'.charCodeAt(0),'Z'.charCodeAt(0)),
         "number": RandomFactory('0'.charCodeAt(0),'9'.charCodeAt(0)),
         "symbol":RandomFactory('!'.charCodeAt(0),'/'.charCodeAt(0))
       }
     }
  },
  methods: {
    gen : function() {
       //construct methods into a ring
       let tail = new Node(this.pmap["lower"])
       let head = tail
       for(let i=0;i<this.pattern.length;i++) {
          tail.next = new Node(this.pmap[this.pattern[i]])
          tail = tail.next
       }
       tail.next = head

       this.randstr = ""
       for(let i=this.length;i>0;i--) {
           this.randstr += String.fromCharCode(head.element())
           head = head.next
       }
    }
  }
}

class Node { 
    constructor(element) 
    { 
        this.element = element; 
        this.next = null
    }
} 



function RandomFactory(min,max){
    min = Math.ceil(min);
    max = Math.floor(max+1);
    return ()=>{
      return Math.floor(Math.random() * (max - min)) + min
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
