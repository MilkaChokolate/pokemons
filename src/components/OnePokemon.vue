<template>
<div>
  <div @click="openModal" class="one-pokemon">
    <h1>{{ pokemon.name }}</h1>
  </div>
  <modal-window :modalIsOpen="modalIsOpen" v-model:show="modalIsOpen">
    <div class="modal-window-content">
      <div>
        <h2>Name:</h2>
        <div>{{infoAboutPokemon.name}}</div>
      </div>
      <div>
        <img :src="this.infoAboutPokemon.sprites.front_default" style="width:230px; height:230px"/>
      </div>
      <div>
        <h2>Abilities:</h2>
        <div v-for="item in infoAboutPokemon.abilities" :key="item.ability.name">{{item.ability.name}}</div>
      </div>
      <div>
        <h2>Forms:</h2>
        <div v-for="item in infoAboutPokemon.forms" :key="item.name">{{item.name}}</div>
      </div>
      <div>
        <h2>Height:</h2>
        <div>{{infoAboutPokemon.height}}</div>
      </div>
      <div>
        <h2>Weight:</h2>
        <div>{{infoAboutPokemon.weight}}</div>
      </div>
      <div>
        <h2>Types:</h2>
        <div v-for="item in infoAboutPokemon.types" :key="item.type.name">{{item.type.name}}</div>
      </div>
      <div>
        <h2>Stats:</h2>
        <div v-for="item in infoAboutPokemon.stats" :key="item.stat.name">{{item.stat.name}}:{{item.base_stat}}</div>
      </div>
    </div>
  </modal-window>
</div>
</template>

<script>
import ModalWindow from "@/components/UI/ModalWindow";
import axios from "axios";
export default {
  name: "OnePokemon",
  components: {ModalWindow},
  data() {
    return {
      modalIsOpen: false,
      infoAboutPokemon: {}
    }
  },
  props: {
    pokemon: {
      type: Object,
    }
  },
  methods: {
    async fetchUrl() {
      try {
        const response = await axios.get(this.pokemon.url);
        console.log(response.data);
        this.infoAboutPokemon = response.data;
        console.log(this.infoAboutPokemon.abilities)
      } catch (e) {
        alert('error');
      }
    },
    openModal() {
      this.fetchUrl();
      this.modalIsOpen = true
    }
  },
}
</script>

<style scoped>

.one-pokemon {
  width: 10%;
  min-width: 200px;
  height: 5vh;
  min-height: 100px;
  margin: 15px;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #2c3e50;
  color: white;
}
.modal-window-content{
  background: white;
}
h2 {
  padding: 0;
  margin: 0;
}
</style>