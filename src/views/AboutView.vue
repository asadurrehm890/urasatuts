<script>

import socialicon from '../components/social.vue'

import axios from "axios"

export default {

components: {
socialicon
},
data(){
   return{
      page:[],
   }
},
mounted() {

    axios
        .post("https://urasaapi.com/api/showpage", {id : "1"})
        .then((response) => {
             console.log(response.data.data.content);
            this.page = response.data.data;


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
    <h4 class="text-center text-white ">{{page.title}}</h4>

  </section>
  <section class="content">
     <div class="container">

      <div v-html="page.content"></div>
      <div class="bc1 text-center card abcard border-0 mx-auto p-3">
      <h5 class="text-center text-white">Follow Me</h5>
       <socialicon color="text-white" />
      </div>
      </div>
  </section>

  </main>
</template>
<style>
.banner{
padding-top:50px;
padding-bottom:50px;
}
.content{
padding-top:50px;
padding-bottom:50px;
}
.abcard{
max-width:600px;
}

</style>
