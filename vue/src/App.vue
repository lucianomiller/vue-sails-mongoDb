<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <div >
    <div>
    <Cartas v-show="show"  />
    </div>

    <Button label="Show saved" @click="onClick()" />
    <div v-show="!show" v-for="user in users" :key="user.id" >      

            <Card style="width: 25em " >
                <template #header>
                    
                    <img v-bind:src=" user.image" /> 
                </template>
                <template #title>
                    <p>{{user.name}} {{user.lastname}}</p>
                    
                </template>                
                <template #content >
                </template>
                <!-- <template #footer>
                    <Button icon="pi pi-check" label="Save" @click="onClick()" />
                    <Button icon="pi pi-times" label="Reroll" class="p-button-secondary" style="margin-left: .5em" @click="reRoll()"/>
                </template> -->
            </Card>
  </div>
  </div>

</template>

<script>
/* import HelloWorld from './components/HelloWorld.vue' */
import Cartas from "./components/Cartas.vue"
import Button from 'primevue/button';
import axios from "axios"


export default {
  name: 'App',
  components: {
    /* HelloWorld */
    Cartas,
    Button
  },
  methods:{
    onClick(){
      this.show=!this.show
      axios.get("http://localhost:1337/user")
            .then(resp=>{
                console.log(resp.data)
                this.users=resp.data
            })
      console.log(this.show)
    }

  },
  data(){
    return{
      show:false,
      users:{}
    }
  }
}
</script>

<style  >

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
  margin: 20px;
  
}
body{
  background: black;
}
div{
 margin: 1px;
}
 

</style>
