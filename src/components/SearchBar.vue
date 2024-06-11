<template>
    <v-container>
        <v-row justify="center">
            <v-col cols="4">
                <v-text-field label="Ingrese el pokémon..." type="text" v-model="pokemon"></v-text-field>
            </v-col>
            <v-col cols="1">
                <v-btn color="primary" size="x-large" @click="searchPokemon()"><v-icon dark>mdi-magnify</v-icon></v-btn>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            pokemon: null
        }   
    },
    methods: {
        searchPokemon() {
            axios.get(`https://pokeapi.co/api/v2/pokemon/${this.pokemon}/`)
            .then(response => {
                localStorage.setItem('pokemon', JSON.stringify(response.data));
            })
            .catch((error) => {
                if (error.response) {
                    // El servidor respondió con un estado fuera del rango 2xx
                    if (error.response.status === 404) {
                        alert("No se encontró el pokémon ingresado!");
                    } 
                    else {
                        alert(`Error: ${error.response.status} - ${error.response.statusText}`);
                    }
                } 
                else if (error.request) {
                    // La solicitud fue hecha pero no se recibió respuesta
                    alert("No se recibió respuesta del servidor. Inténtalo de nuevo más tarde.");
                } 
                else {
                    // Algo sucedió al configurar la solicitud que provocó un error
                    alert("Error al realizar la solicitud. Inténtalo de nuevo.");
                }
                console.log(error);
            });
            this.pokemon = null;
        }
    }
}
</script>