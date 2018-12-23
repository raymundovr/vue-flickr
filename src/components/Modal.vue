<template>
  <div id="modal" class="modal">   
    <a href="#" class="close" @click="closed">X Close</a>
    <img :src="url" />    
  </div>
</template>
<script>
export default {
  props: {
    url: String
  },
  methods: {
    closed: function() {
      this.$emit('modal-closed');
    }
  }
}
</script>
<style scoped>
.modal {
  position: fixed;
  display: block;
  align-self: center;
  z-index: 100;
  box-shadow: 20px 20px 50px 15px grey;
  top: 20%;
  left: 30%;
  background-color: white;
  padding: 1rem;
}
.modal > img {
  display: block;
}
.close {
  font-size: 1rem;
  color: red;
  text-align: center;
}
</style>
