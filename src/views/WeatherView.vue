<template>
<div class="about">
    <h1 class="text-subtitle-4 text-center">This is an weather page</h1>
    <hr><br>
    <div>

        <v-container>
            <v-row>
                <v-col cols="12" sm="6">
                    <v-text-field label="Write a location" v-model="value"></v-text-field>
                </v-col>

                <v-col cols="12" sm="6">
                    <v-btn fluid depressed color="primary" @click="handleEvent"> Search </v-btn>
                </v-col>
            </v-row>
        </v-container>
        <!-- <v-card v-if="show" align="center" width="400"> 
        <img  :src="image" alt="foto" width=200 />
        <h1 >Country : {{country}}</h1>
        <h1 >{{degree}} °C</h1>
        <h1 >{{location}}</h1>
        </v-card> -->
        <v-card v-if="show" class="mx-auto" max-width="368">
            <v-card-item :title="location" align="center">
                <template v-slot:subtitle>
                </template>
            </v-card-item>

            <v-card-text class="py-0">
                <v-row align="center" no-gutters>
                    <v-col class="text-h2" cols="6">
                        {{degree}}&deg;C
                    </v-col>

                    <v-col cols="6" class="text-right">
                        <v-icon color="error" icon="mdi-weather-hurricane" size="88"></v-icon>
                    </v-col>
                </v-row>
            </v-card-text>

            <div class="d-flex py-3 justify-space-between">
                <v-list-item density="compact" prepend-icon="mdi-weather-windy">
                    <v-list-item-subtitle>{{wind_degree}} km/h</v-list-item-subtitle>
                </v-list-item>

                <v-list-item density="compact" prepend-icon="mdi-weather-pouring">
                    <v-list-item-subtitle>{{humidity}}%</v-list-item-subtitle>
                </v-list-item>
            </div>
            <div class="d-flex py-3 justify-space-between">
                <v-img :src="image" max-width="500" max-height="300"></v-img>

            </div>

        </v-card>
        <h1>{{hata}}</h1>
    </div>
</div>
</template>

<script lang="ts">
import {
    defineComponent
} from '@vue/runtime-core'
import axios from 'axios'
export default defineComponent({
    data() {
        return {
            value: "",
            location: " ",
            show: false,
            region: "",
            image: "",
            degree: "",
            country: "",
            humidity: "",
            wind_degree: "",
           hata:[]
        }
    },
    methods: {
        handleEvent(): any {
            //console.log(this.value);
     try {
      axios.get(`http://api.weatherapi.com/v1/current.json?key=074dad7aa42345a9832135725223110&q=${this.value}`)
                .then((response) => {
                    //console.log(response)
                    const data = response;
                    this.show = true
                    this.location = data.data.location.name
                    this.region = data.data.location.region
                    this.image = data.data.current.condition.icon
                    this.degree = data.data.current.temp_c
                    this.country = data.data.location.country
                    this.humidity = data.data.current.humidity
                    this.wind_degree = data.data.current.wind_degree
                    this.value = ""
                })
     } 
     catch (error) {
     console.log(error)
      
     }
           
        }
    },

})
</script>

<style scoped>

</style>
