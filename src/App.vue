<template>
  <poke-list></poke-list>
</template>

<script>
import PokeList from "@/components/PokeList";

export default {
  name: 'App',
  components: {
    PokeList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background: url(images/pokemon-background.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
}
</style>
