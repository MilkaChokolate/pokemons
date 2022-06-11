<template>
  <div v-show="isActive">
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

</style>