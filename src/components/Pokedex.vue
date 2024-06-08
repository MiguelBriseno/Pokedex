<template>
  <v-container>
    <v-card class="mx-auto my-4" max-width="450" v-if="pokemon != null" id="pokedex">
      <v-card-title class="d-flex justify-space-between align-center">
        <strong>{{ pokemon.name.toUpperCase() }}</strong>
        <span>N.º {{ formatearA5Digitos(pokemon.id) }}</span>
      </v-card-title>
      <v-spacer></v-spacer>
      <v-card-text class="d-flex justify-center align-center" id="image">
        <v-img :src="pokemon.sprites.front_default"></v-img>
      </v-card-text>
      <v-card-text id="info">
        <p class="d-flex justify-space-around align-center">
          <span>Height: {{ formatearPeso(pokemon.height) }} m</span>
          <span>Weight: {{ formatearPeso(pokemon.weight) }} kg</span>
        </p>
        <p class="text-md-center">Ability: {{ pokemon.abilities[0].ability.name }}</p><br>
        <v-card-subtitle>BASE STATS</v-card-subtitle>
        <p class="d-flex justify-space-between align-center">
          <span>HP: {{ pokemon.stats[0].base_stat }}</span>
          <span>ATTACK: {{ pokemon.stats[1].base_stat }}</span>
        </p>
        <p class="d-flex justify-space-between align-center">
          <span>DEFENSE: {{ pokemon.stats[2].base_stat }}</span>
          <span>SPECIAL ATTACK: {{ pokemon.stats[3].base_stat }}</span>
        </p>
        <p class="d-flex justify-space-between align-center">
          <span>SPECIAL DEFENSE: {{ pokemon.stats[4].base_stat }}</span>
          <span>SPEED: {{ pokemon.stats[5].base_stat }}</span>
        </p><br>
        <v-btn block :color="pokemon.types[0].type.name == 'normal' ? 'white' : pokemon.types[0].type.name == 'fire' ? 'red' : pokemon.types[0].type.name == 'water' ? 'indigo' : pokemon.types[0].type.name == 'electric' ? 'yellow' : pokemon.types[0].type.name == 'grass' ? 'green' : pokemon.types[0].type.name == 'ice' ? 'light-blue-darken-4' : pokemon.types[0].type.name == 'fighting' ? 'orange-darken-4' : pokemon.types[0].type.name == 'poison' ? 'deep-purple-accent-4' : pokemon.types[0].type.name == 'ground' ? 'orange-accent-3' : pokemon.types[0].type.name == 'flying' ? 'light-blue-darken-1' : pokemon.types[0].type.name == 'psychic' ? 'deep-purple-accent-2' : pokemon.types[0].type.name == 'bug' ? 'light-green-darken-3' : pokemon.types[0].type.name == 'rock' ? 'lime-darken-4' : pokemon.types[0].type.name == 'ghost' ? 'deep-purple' : pokemon.types[0].type.name == 'dragon' ? 'indigo-darken-4' : pokemon.types[0].type.name == 'dark' ? 'grey-darken-4' : pokemon.types[0].type.name == 'steel' ? 'grey-darken-1' : 'pink'">{{ pokemon.types[0].type.name }}</v-btn>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      pokemon: null,
      intervalId: null
    };
  },
  created() {
    this.checkLocalStorage();
    this.intervalId = setInterval(this.checkLocalStorage, 1000); // Revisa cada segundo
  },
  beforeDestroy() {
    clearInterval(this.intervalId);
  },
  methods: {
    checkLocalStorage() {
      const pokemonData = localStorage.getItem('pokemon');
      if (pokemonData) {
        this.pokemon = JSON.parse(pokemonData);
      } else {
        this.pokemon = null;
      }
    },
    formatearA5Digitos(numero) {
      return numero.toString().padStart(5, '0');
    },
    formatearPeso(peso) {
      // Dividir el peso por 10 para obtener el valor deseado
      var pesoFormateado = (peso / 10).toFixed(1);
      return pesoFormateado;
    }
  }
};
</script>

<style lang="scss" scoped>
#pokedex{
  background-color: red;
}
#image{
  background-color: white;
  width: 50%;
  display: block;
  margin: 0 auto;
}
#info{
  width: 80%;
  margin: 1rem auto;
  background-color: white;
  color: rgb(32, 32, 32);
  font-weight: 600;
}
</style>