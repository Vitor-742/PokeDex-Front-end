<template>
  <div v-on:click="addInfo">
    <p>
      {{
        poke.species.name.charAt(0).toUpperCase() + poke.species.name.slice(1)
      }}
    </p>
    <img v-bind:src="poke.sprites.front_default" />
    <ul>
      <li v-for="typ in poke.types" v-bind:key="typ">
        <p>{{ typ.type.name }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PokeCard",
  props: ["poke"],
  methods: {
    addInfo() {
      this.$emit("add-info", {
        poke: this.poke,
      });
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-inline-start: 0;
}
</style>
