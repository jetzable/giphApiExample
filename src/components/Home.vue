<script>
import { log } from 'util';
export default {
  name: 'Home',
  data(){
    return{
      giphCount: 5,
      doggos: []
    }
  },
  created(){
   this.getGifs()   
  }, 
  methods: {
   getGifs(){
     for(let i=0; i< this.giphCount; i++){  
       const search = 'dog'
    const key = process.env.VUE_APP_API_KEY
    const url = `http://api.giphy.com/v1/gifs/random?tag=dog&api_key=${key}&limit=5`
    fetch(url)
    .then((res) => res.json())
    .then((giphyresp) => {
      console.log(giphyresp);
      
      const gifObj = {
        url: giphyresp.data.image_mp4_url,
        title:giphyresp.data.title,
        id: giphyresp.data.id
      }
this.doggos.push(gifObj)
    })
    .catch((err) => {
      console.log(err);
      
    })
     }
   }
  }
}
</script>

<template>
  <div class="container">
    <h1 class="title">I feel Great!!!</h1>
    <div class="grid" v-if="doggos.length > 0">
        <video v-for="gif in doggos" :key="gif.id" :src="gif.url" autoplay loop class="grid-item"></video>
    </div>
  </div>
</template>
<style  scoped>
.container{
  width: 100%;
  height: 100%;
  padding: 2rem;
  background-color: black
}
.title{
  text-align: center;
  color: #F9DC5C
}
.grid{
  margin: 1rem;
  text-align: center;
  height: 100%;
}
.grid-item{
  padding: .5rem;
  width: auto;
  height: 350px;
}
</style>