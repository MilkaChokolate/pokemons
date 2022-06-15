<template>
  <div class="oneAbility">
    <h4 @click="show = !show" @click.once="fetchAbility()">{{ability.name}}&#10033;</h4>
    <div v-if="show">
      <div  class="info-about-ability">{{abilityInfo.effect_entries[1].effect}}</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "OneAbility",
  props: {
    ability: Object
  },
  data() {
    return {
      show: false,
      abilityInfo: {}
    }
  },
  methods: {
  //При открытии спойлера получаем данные о конкретном навыке покемона (получаем один раз)
    async fetchAbility() {
      try {
        const response = await axios.get(this.ability.url);
        this.abilityInfo = response.data;
        console.log(response.data)
      } catch (e) {
        alert("Error")
      }
    }
  }
}
</script>

<style scoped>
.oneAbility h4 {
  margin: 5px;
  width: 300px;
  height: fit-content;
  text-decoration: underline dotted blue;
  cursor: pointer;
}
.info-about-ability{
  width: 300px;
  text-align: center;
}
</style>
