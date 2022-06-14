<template>
  <div v-show="isActive" class="pokemon-list">
    <div v-for="pokemon in onePaginate" :key="pokemon.name">
    <one-pokemon :pokemon="pokemon"></one-pokemon>
  </div>
  </div>
</template>

<script>
import OnePokemon from "@/components/OnePokemon";
export default {
  name: "PaginationPage",
  components: {OnePokemon},
  props: {
    onePaginate: {
      type: Array
    },
    isActive: {
      type: Boolean
    }
  }
}
</script>

<style scoped>

.pokemon-list{
  display: flex;
  flex-wrap: wrap;
  width: 85%;
  text-align: center;
  min-width: 300px;
  justify-content: center;
}

</style>