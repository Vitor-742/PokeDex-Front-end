<template>
  <section>
    <ul>
      <li v-for="poke in pokemonEvolutions" v-bind:key="poke">
        <PokeCard v-bind:poke="poke" v-on:add-info="addInfo"></PokeCard>
      </li>
    </ul>
    <ul>
      <li v-for="stat in pokemonStats" v-bind:key="stat">
        <p>{{ stat.stat.name }}</p>
        <p>{{ stat.base_stat }}</p>
      </li>
    </ul>
  </section>
</template>

<script>
import PokeCard from "./PokeCard";
export default {
  name: "PokemonsTable",
  props: ["pokemonEvolutions"],
  components: {
    PokeCard,
  },
  methods: {
    addInfo(pokeProxy) {
      const { poke } = JSON.parse(JSON.stringify(pokeProxy));
      this.pokemonStats = poke.stats;
      console.log(poke.stats);
    },
  },
  data() {
    return {
      pokemonStats: [],
    };
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 20px;
  border-style: solid;
  border-radius: 10px;
  border-width: 2px;
  box-shadow: 5px 8px;
  min-width: 100px;
  min-height: 100px;
  background-color: white;
}
</style>
