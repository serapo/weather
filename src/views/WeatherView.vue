<template>
<div class="about">
    <h1 class="text-subtitle-4 text-center">This is an weather page</h1>
    <div>
        <!-- <input type="text" class="text"> -->
        <v-text-field label="Write a location" v-model="value" ></v-text-field>
        <v-btn fluid depressed color="primary" @click="handleEvent"> Search </v-btn>

        <v-card v-if="show" align="center" width="400"> 
        <img  :src="image" alt="foto" width=200 />
        <h1 >Country : {{country}}</h1>
        <h1 >{{degree}} °C</h1>
        <h1 >{{location}}</h1>
        </v-card>
    </div>
</div>
</template>

<script lang="ts">
import { defineComponent } from '@vue/runtime-core'
import axios from 'axios'
export default defineComponent ({
  data() {
    return {
       value : "",
       location:" ",
       show: false,
       region:"",
       image:"",
       degree:"",
       country:""
      }
  },
  methods :{
    handleEvent():any{
      console.log(this.value);
      
      axios
      .get(`http://api.weatherapi.com/v1/current.json?key=074dad7aa42345a9832135725223110&q=${this.value}`)
      .then((response) => {
        console.log(response)
        const data=response;
        this.show=true
        this.location=data.data.location.name
        this.region=data.data.location.region
        this.image=data.data.current.condition.icon
        this.degree=data.data.current.temp_c
        this.country=data.data.location.country
        this.value=""
      })
    }
  },
 
    
  
  
})
</script>
<style scoped>

</style>
