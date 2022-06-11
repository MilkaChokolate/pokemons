<template>
<div class="modal" v-if="modalIsOpen" @click="hideModalWindow">
  <div @click.stop class="modal-window-content">
    <div class="close" @click="hideModalWindow">X</div>
    <slot></slot>
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
  min-height: 650px;
  min-width: 650px;
  margin: auto;
  z-index: 3;
}
.close {
  color: black;
  cursor: pointer;
  font-size: 42px;
  float: right;
}
</style>