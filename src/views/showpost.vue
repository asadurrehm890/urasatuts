<script>
import facebookicon from '../components/icons/facebook.vue'
import twittericon from '../components/icons/twitter.vue'
import instaicon from '../components/icons/instagram.vue'
import linkedinicon from '../components/icons/linkedin.vue'
import pinteresticon from '../components/icons/pinterest.vue'

import axios from "axios";


export default {
components: {
twittericon ,facebookicon, instaicon, linkedinicon, pinteresticon
},

       data() {
           return {
               posts: [],
               errors: [],

           };
       },


       mounted() {

           axios
               .post("https://urasaapi.com/api/show", {id: this.$route.params.id})
               .then((response) => {
                    console.log(response.data.data.content);
                   this.posts = response.data.data;


               })
               .catch((e) => {
                   this.errors.push(e);
               });
       }
   }

</script>

<template>
  <main>
  <section class="banner bc2">
    <h4 class="text-center text-white ">Latest Posts</h4>
    </section>

    <section class="posts">
       <div class="container">
       <div class="row">

       <div class="col-lg-8 col-md-12 col-sm-12">
          <a href="/" class="my-3 btn btn-primary bc1">Back</a>

          <h2>{{posts.title}}</h2>

           <div v-html="posts.content"></div>


        </div>
        <div class="col-lg-4 col-md-12 col-sm-12 bi1 position-relative">
           <div class="bg-dark w-100 h-100 position-absolute tint"></div>

            <div class="card subscard my-4 p-4 bg-dark">
               <h5 class="text-center text-white">Subscribe Us</h5>
               <h5 class="text-center text-white text-capitalize">to get latest Updates</h5>


               <input placeholder="Email Address" type="email" class="mt-4 ps-4 rounded-pill shadow p-2 border">

               <button class="btn btn-dark bc1 op rounded-pill mt-2">Subscribe</button>



            </div>

            <div class="card subscard my-4 p-4 bg-dark">
               <h5 class="text-center text-white">Follow Us</h5>
               <div class="social text-center mt-2">
                   <a href="" class="c1 op me-2"><facebookicon /></a>
                   <a href="" class="c1 op mx-2"><twittericon /></a>
                   <a href="" class="c1 op mx-2"><instaicon /></a>
                   <a href="" class="c1 op mx-2"><linkedinicon /></a>
                   <a href="" class="c1 op mx-2"><pinteresticon /></a>
               </div>

            </div>




        </div>

        </div>
        </div>
    </section>



  </main>
</template>
<style>
.card-img{
width: 100%;
height: 400px;
object-fit: cover;
}
.banner{
padding-top:50px;
padding-bottom:50px;
}
.posts{
padding-top:50px;
padding-bottom:50px;
}
.posts .card{
cursor:pointer;
  max-width:700px;
  width:100%;
  height:400px;
  margin-bottom:50px;

}

.subscard{
   height:auto !important;
   cursor:default !important;
}

.wh25{
width:50px;
height:50px;

}

.tint{
left:0 !important;
opacity:0.75;
}

</style>
