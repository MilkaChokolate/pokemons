<template>
<div class="modal" v-if="modalIsOpen" @click="hideModalWindow">
  <div @click.stop class="modal-window-content">
    <slot></slot>
    <div class="close" @click="hideModalWindow">X</div>
  </div>

</div>
</template>

<script>
export default {
  props: {
    modalIsOpen: {
      type: Boolean
    }
  },
  methods: {
    hideModalWindow(){
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.modal {
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
  z-index:2;
}
.modal-window-content{
  padding: 15px;
  display: flex;
  margin: auto;
  text-align: center;
  justify-content: center;
  z-index: 3;
  min-width: 300px;
  background: white;
  border-radius: 5px;
  border: 3mm ridge #2c3e50;
}
.close {
  color: black;
  cursor: pointer;
  font-size: 36px;
}
</style>