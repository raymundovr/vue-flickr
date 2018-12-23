<template>
  <div class="flickr">    
    <input v-model="keyword" @keyup.enter="submit" />
    <button @click="submit">Search</button>
    <h3 v-show="isLoading">Loading...</h3>
    <div id="results" class="results">
      <div v-for="photo in photos" :key="photo.id" @click="setActive(photo.url)">
        <img :src="photo.url" :alt="photo.title" />
      </div>
    </div>
  </div>  
</template>

<script>
import {getAPIURL, getPhotosFromResponse} from '../utils.js';
import log from '../mixins/log.js';
export default {
  name: "Flickr",  
  data: function() {
    return {
      keyword: "",
      photos: [],
      isLoading: false,
      activeUrl: '',
    };
  },
  mixins: [log],
  methods: {
    submit: async function() {
      let apiUrl = getAPIURL(this.keyword);     
      this.l(apiUrl); 
      try {
        this.isLoading = true;
        let response = await fetch(apiUrl);        
        let jsonResponse = await response.json();
        this.photos = getPhotosFromResponse(jsonResponse);        
      } catch (ex) {
        this.l('On rendering JSON', ex);
      }
      this.isLoading = false;
    },
    setActive: function (url) {      
      this.$emit('picture-clicked', url);      
    }
  },
  props: {
    apiKey: String
  }
}
</script>

<style scoped>
.results {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 1rem;
}

.results > div {
  flex: 1 1 200px;
}

.results > div > img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

</style>
