<template>
  <div id="app">
    <h3>Search on Flickr</h3>
    <Flickr v-on:picture-clicked="pictureClicked"/>
    <Modal v-show="showModal" v-bind:url="modalUrl" v-on:modal-closed="closeModal" />
  </div>
</template>

<script>

import Flickr from './components/Flickr.vue';
import Modal from './components/Modal.vue';
import log from './mixins/log.js';

export default {
  name: 'app',
  mixins: [log],
  data: function () {
    return {
      showModal: false,
      modalUrl: '',
    }
  },
  created() {
    //this.l('Hi!');
  },
  components: {
    Flickr,
    Modal
  },
  methods: {
    pictureClicked: function(url) {
      this.showModal = true;
      this.modalUrl = url;
    },
    closeModal: function() {
      this.showModal = false;
      this.modalUrl = '';
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
