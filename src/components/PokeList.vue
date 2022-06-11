<template>
  <div class="pokemons-list">
    <input type="text" v-model="searchQuery">
    <div v-for="(onePaginate, index) in searchedPosts" :key="onePaginate">
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

export default {
  name: "PokeList",
  components: {PaginationPage},
  data() {
    return {
      pokemons: [],
      searchQuery: '',
      amountPages: 0,
      currentPage: +localStorage.getItem("currentPage") || 1,
      limit: 100,
      maxOnOnePage: 10,
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
  },
  mounted() {
    this.fetchPokemons();
  },
  computed: {
      searchedPosts() {
        let results = [];
        let arr = this.pokemons.flat().filter(pokemon => pokemon.name.toLowerCase().includes(this.searchQuery.toLowerCase()))
        for (let i = 0; i < arr.length; i += this.maxOnOnePage) {
          results.push(arr.slice(i, i + this.maxOnOnePage));
        }
        return results
    }
  }
}
</script>

<style scoped>
.pokemons-list{
  display: flex;
  align-items: center;
  flex-direction: column;
}
.pages-wrapper{
  display: flex;
}
.page-number{
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
}
.current-page {
  border: 2px red solid;
  padding: 10px;
  cursor:pointer;
}
</style>