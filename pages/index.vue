<template>
  <b-carousel
  id="carousel"
  v-model="slide"
  :interval="3500"
  controls
  indicators
  style="text-shadow: 1px 1px 2px #333"
  @sliding-start="onSlideStart"
  @sliding-end="onSlideEnd"
  >
  <div v-for="image in Images" :key="image.id">
    <b-carousel-slide :img-src="image.url">
    </b-carousel-slide>
  </div>
  </b-carousel>


</template>
 
<script>
import axios from 'axios'

export default {
  data() {
    return {
      Images: [],
      slide: 0,
      sliding: null
    }
  },

  methods: {
    onSlideStart(slide) {
      this.sliding = true
    },
    onSlideEnd(slide) {
      this.sliding = false
    }
  },

  async asyncData(){
    try{
      let { data } = await axios.get(`https://jsonplaceholder.typicode.com/photos`)
      return {Images: data}

    } catch (err){
      console.log(err )

    }
  }
}
</script>  

<style> 
 
</style>
