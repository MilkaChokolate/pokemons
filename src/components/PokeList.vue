<template>
  <div class="wrapper">
    <poke-input v-model="searchQuery"></poke-input>
    <div v-for="(onePaginate, index) in searchedPosts" :key="onePaginate" class="paginate-wrapper">
      <pagination-page :onePaginate="onePaginate" :isActive="index + 1 === this.currentPage"></pagination-page>
    </div>
    <div class="pages-wrapper">
      <div v-for="page in amountPages"
           :key="page"
           class="page-number"
           @click="changePage(page)"
           :class="{'current-page': page === this.currentPage}">
        {{page}}
      </div>
    </div>
  </div>

</template>

<script>
import axios from 'axios'
import PaginationPage from "@/components/PaginationPage";
import PokeInput from "@/components/UI/PokeInput";

export default {
  name: "PokeList",
  components: {PaginationPage, PokeInput},
  data() {
    return {
      pokemons: [],
      searchQuery: '',
      amountPages: 0,
      currentPage: +localStorage.getItem("currentPage") || 1,
      limit: 100,
      maxOnOnePage: 12,
      offset: 0
    }
  },
  methods: {
    async fetchPokemons() {
      let array = [];
      try {
        const response = await axios.get('https://pokeapi.co/api/v2/pokemon?', {
          params: {
            limit: this.limit,
            offset: this.offset
          }
        });
        for (let i = 0; i < response.data.results.length; i += this.maxOnOnePage) {
          array.push(response.data.results.slice(i, i + this.maxOnOnePage));
        }
        localStorage.setItem('pokemons', JSON.stringify(array));
        this.pokemons = JSON.parse(localStorage.getItem('pokemons'))
        this.amountPages = this.pokemons.length;
      } catch (e) {
        alert('error');
      }
    },
    changePage(page){
      localStorage.setItem('currentPage', String(page))
      this.currentPage = page;
    },
    changePaginationOnSearch(arr){
      console.log(arr, arr.length)
      this.amountPages = Math.ceil(arr.length / this.maxOnOnePage);
      this.currentPage = 1;
    }
  },
  mounted() {
    this.fetchPokemons();
  },
  computed: {
      searchedPosts() {
        let results = [];
        let arr = this.pokemons.flat().filter(pokemon => pokemon.name.toLowerCase().includes(this.searchQuery.toLowerCase()))
        this.changePaginationOnSearch(arr);
        for (let i = 0; i < arr.length; i += this.maxOnOnePage) {
          results.push(arr.slice(i, i + this.maxOnOnePage));
        }
        return results
    }
  }
}
</script>

<style scoped>
.wrapper{
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}
.paginate-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.pages-wrapper{
  display: flex;
  flex-wrap: wrap;
}
.page-number{
  border: 1px solid black;
  padding: 8px;
  background: white;
  cursor: pointer;
  border-radius: 5px;
  margin: 4px;
  font-size: 22px;
}
.current-page {
  font-size: 24px;
  border: 2px red solid;
  padding: 8px;
  border-radius: 5px;
  margin: 4px;
  background: white;
  cursor:pointer;
}
@media (max-width: 768px) {
  .wrapper{
    height: fit-content;
  }
  .paginate-wrapper{
    margin: 0;
  }
}
</style>