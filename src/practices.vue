<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <div>
    HelloWorld I am from GaadMaiyaki{{name}}
  </div>
  <div>
    this is length {{ arrLength }}
  </div>
  <div v-html="name"></div>
  <div v-text="name"></div>
  <input v-model="name"/>
  <div>{{randc}}</div>
  <div>{{randm()  }}</div>
  <button @click="pushData()">push</button>

  <div>{{fn}} {{ln}}</div>
  this is the new done computed<div v-text="fnC"></div>
  this is the new done computed<div v-text="fnM()"></div>
  <!-- to invoke the a method with a return value needs something like this fnM(), but for computed just needs fnC -->
  <div v-text="fullname"></div>

  <button @click="setFullname()">set fullname</button>

</template>


<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  // name: 'App',
  // components: {
  //   HelloWorld
  // }
  
  data() {
   return{
     name: "Peter Maiyaki",
     fn: "Soyebo",
     ln: "Temitope",
     arr: ['me', 'you', 'they', 'that', 'yes'],
   }
  },

  //computed properties by default only have getters, however we can define setters too
  //computed run only when the dependency changes, cacehed, used as property in place of data
  //methods are invoked by v-on event binding, not cached, run when update occurs, have getters and setters
  computed:{
    arrLength() {
      //note that here, the dc heroes helped us to calculate the length of the array, whereas we can use it straight with the 
      //data, but we would need to type "arr.length" very time that we need to reuse it
      return this.arr.length+`${this.arr.length > 1 ? ' heroes' : ' hero' }`;
    },
    randc(){

      //note here that if we only return a math.random, nothing is going to happen, i.e. it won't ne recomputed. however,giving it the length of a arr as a dependency would only only make it generate another random number when the length of that particular array changes, note that when i changed the dependency as the name, it keeps updating every time, i type a new thing
      
      return this.arr.length + Math.random();
    },

    fnC(){
      return `${this.fn} ${this.ln}`;
    },
    //setting a getter in the computed properties
    //in conclusion here, the computed property limits the number of states that we have in our data, it's been handle by computed property
    fullname:{
      get() {
        return `Fullname is: ${this.fn} ${this.ln}`;
      },
      set(fullname){
        [this.fn, this.ln] = fullname.split(" ");
      }
    }
  },
  methods:{
    pushData(){
      this.arr.push(this.name);
    },
    addMe(){
      alert('i am a add!');
    },
    randm(){
      return Math.random();
    },
    fnM(){
      return `${this.fn} ${this.ln}`;
    },
    setFullname(){
      //instead of directly setting and returning the first and last name, we have used the computed properties, to compute this portions
      this.fullname = "hello, peter! ";
    }
  },

  

}
  
  

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
