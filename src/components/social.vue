<script>
import facebookicon from './icons/facebook.vue'
import twittericon from './icons/twitter.vue'
import instaicon from './icons/instagram.vue'
import linkedinicon from './icons/linkedin.vue'
import pinteresticon from './icons/pinterest.vue'
import axios from "axios";

export default {
components: {
twittericon ,facebookicon, instaicon, linkedinicon, pinteresticon
},

props: {
   color:String,
 },

 data(){
   return{
     links:null,
   }
 },

 mounted() {
     axios
         .get("https://urasaapi.com/api/social")
         .then((response) => {
              console.log(response.data);
              this.links=response.data.data;

         })
         .catch((e) => {

         });
 }

}
</script>

<template>


<div class="social" v-if="links">
    <a :href="links[0].url" :class="color" class=" op me-2"><facebookicon /></a>
    <a :href="links[1].url" :class="color" class=" op mx-2"><twittericon /></a>
    <a :href="links[2].url" :class="color" class=" op mx-2"><instaicon /></a>
    <a :href="links[3].url" :class="color" class=" op mx-2"><linkedinicon /></a>
    <a :href="links[4].url" :class="color" class=" op mx-2"><pinteresticon /></a>
</div>

</template>

<style>

</style>
