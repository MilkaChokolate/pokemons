<template>
  <div>
    <div @click.once="fetchUrl()" @click="modalIsOpen = true" class="one-pokemon">
      <h1>{{ pokemon.name }}</h1>
    </div>
    <modal-window :modalIsOpen="modalIsOpen" v-model:show="modalIsOpen">
      <div class="info-about-pokemon">
        <div>
          <div class="image">
            <img :src="this.infoAboutPokemon.sprites.front_default"/>
          </div>
          <div class="stats">
            <h2>Stats:</h2>
            <div v-for="item in infoAboutPokemon.stats" :key="item.stat.name" style="display: flex;">
              <div
                  style="padding: 5px; border-top-left-radius: 10px; border-bottom-left-radius: 10px; background: #e61212; color:white">
                {{ item.stat.name }}
              </div>
              <div
                  style="padding: 5px; border-top-right-radius: 10px; border-bottom-right-radius: 10px; background: #f4fa43; color: black">
                {{ item.base_stat }}
              </div>
            </div>
          </div>
          </div>

          <div>
            <div class="name">
              <div class="coloredText" style="font-weight: bold">{{ infoAboutPokemon.name }}</div>
            </div>
            <div class="forms">
              <h2>Forms:</h2>
              <div  class="coloredText" v-for="item in infoAboutPokemon.forms" :key="item.name">{{ item.name }}</div>
            </div>
            <div class="height">
              <h2>Height:</h2>
              <div class="coloredText">{{ infoAboutPokemon.height }}</div>
            </div>
            <div class="weight">
              <h2>Weight:</h2>
              <div class="coloredText">{{ infoAboutPokemon.weight }}</div>
            </div>
            <div class="types">
              <h2>Types:</h2>
              <div class="coloredText" v-for="item in infoAboutPokemon.types" :key="item.type.name">{{ item.type.name }}</div>
            </div>
            <div class="ability">
              <h2>Abilities:</h2>
              <div v-for="item in infoAboutPokemon.abilities" :key="item.ability.name">
                <one-ability :ability="item.ability">{{ item.ability.name }}</one-ability>
              </div>
            </div>
          </div>
        </div>
    </modal-window>
  </div>
</template>

<script>
import ModalWindow from "@/components/UI/ModalWindow";
import axios from "axios";
import OneAbility from "@/components/OneAbility";
export default {
  name: "OnePokemon",
  components: {OneAbility, ModalWindow},
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
  //Получаем данные о конкретном покемоне
    async fetchUrl() {
      try {
        const response = await axios.get(this.pokemon.url);
        console.log(response.data);
        this.infoAboutPokemon = response.data;
      } catch (e) {
        alert('error');
      }
    }
  }
}
</script>

<style scoped>

.one-pokemon {
  width: 10%;
  min-width: 180px;
  height: 5vh;
  min-height: 100px;
  margin: 15px;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  border-radius: 5px;
  border: 2mm ridge #2c3e50;
  color:#2c3e50;
  cursor: pointer;
}
h2 {
  padding: 0;
  margin: 0;
}
.ability{
  margin-top: 5px;
  height: fit-content;
  min-width: 300px;
  min-height: 180px;
  border-radius: 10px;
  background: #2c3e50;
  color: white;
}
.name {
  border: dotted 1px red;
  border-radius: 5px;
}
.stats{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.info-about-pokemon {
  display: flex;
}
.image img {
  width:230px;
  height:230px
}
.coloredText {
  color:red;
  font-size: 36px;
}
@media (max-width: 768px) {
  .info-about-pokemon{
    flex-direction: column;
    align-items: center;
  }
  .weight, .height{
    display: inline-block;
    margin: 5px;
  }
  .image img {
    width: 180px;
    height: 180px;
  }
  h2 {
    font-size: 18px;
  }
  .coloredText {
    font-size: 18px;
  }
}
</style>
