<template>
    <div class="container">
        <h1 class="my-4">App Météo avec VueJS</h1>

        <div class="form-groupe mb3">
            <label for="position"> <h3>Entrez le nom d'une Ville</h3></label>
            <input v-model="requete" v-on:keypress.enter="goMeteo" type="text" id="position" class="form-control">
        </div>
        <div v-if="temps" class="w-75 m-auto">
            <div class="card text-center p-5 mt-5">
                <h3 class="text-center">Position : {{temps.name}}</h3>
                <p class="texte-affichage"> Temperature : {{temps.main.temp}}°</p>
                <p class="texte-affichage"> Temps : {{temps.weather[0].description}}</p>
            </div>
        </div>
    </div>
</template>


<script>
import axios from 'axios'

export default {
    name: 'Meteo',
    data(){
        return{
            requete: '',
            temps: undefined,
            api_code: '30276a76bd07842a47c29695ac60a17c', //https://home.openweathermap.org/api_keys
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?', //https://openweathermap.org/current
        }
    },
    methods: {
        goMeteo: function(){
            axios
            .get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`)
            .then(response => {
                //console.log(response)
                this.temps=response.data;
            })
            this.requete = ''
            
        }
    }
}
</script>



<style>
    .texte-affichage{
        font-size: 30px;
        font-weight: 300;
        line-height: 1.2;
    }
</style>