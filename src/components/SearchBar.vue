<template>
  <section>
    <input type="text" v-model="pokemonName" />
    <button type="button" v-on:click="SearchPokemon">procurar</button>
    <PokemonsTable v-bind:pokemon-evolutions="pokemonEvolutions" />
  </section>
</template>

<script>
import PokemonsTable from "./PokemonsTable";
export default {
  name: "SearchBar",
  components: {
    PokemonsTable,
  },
  data() {
    return {
      pokemonName: "",
      pokemonEvolutions: [],
    };
  },
  methods: {
    SearchPokemon() {
      let url1 = "https://pokeapi.co/api/v2/pokemon/" + this.pokemonName;
      fetch(url1)
        .then((res) => res.json())
        .then((json) => json.species.url)
        .then((url) =>
          fetch(url)
            .then((res) => res.json())
            .then((json) => json.evolution_chain.url)
            .then((url) =>
              fetch(url)
                .then((res) => res.json())
                .then((json) => {
                  let pokemonEvolutions = json.chain;
                  const arrEvolutions = [pokemonEvolutions.species.name];
                  while (pokemonEvolutions.evolves_to.length == 1) {
                    arrEvolutions.push(
                      pokemonEvolutions.evolves_to[0].species.name
                    );
                    pokemonEvolutions = pokemonEvolutions.evolves_to[0];
                  }
                  this.pokemonEvolutions = [];
                  this.pokemonName = "";
                  arrEvolutions.map((poke) => {
                    fetch("https://pokeapi.co/api/v2/pokemon/" + poke)
                      .then((res) => res.json())
                      .then((json) => this.pokemonEvolutions.push(json));
                  });
                })
            )
        );
    },
  },
};
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
