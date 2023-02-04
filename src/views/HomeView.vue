<script>
import socialicon from '../components/social.vue'


import axios from "axios";


export default {
components: {
socialicon
},

       data() {
           return {
               posts: [],
               errors: [],
               current:1,
               total:0,
               subsemail:'',
               errormessage:'',
               subsmess:''
           };
       },


       mounted() {
           axios
               .get("https://urasaapi.com/api/getposts?page=1")
               .then((response) => {
                    console.log(response.data.count);
                   this.posts = response.data.data.data;
                   this.total=response.data.count;

               })
               .catch((e) => {
                   this.errors.push(e);
               });
       },

       methods:{
          next(){


          if(this.total>10){
              this.total-=10;
             this.current++;

          }
          axios
              .get("https://urasaapi.com/api/getposts?page="+this.current)
              .then((response) => {
                   console.log(response.data.data);
                  this.posts = response.data.data.data;

              })
              .catch((e) => {
                  this.errors.push(e);
              });
               window.scrollTo(0,0);
          },

          prev(){

           if(this.current>=2){
             this.total+=10;
           this.current--;
           }
          axios
              .get("https://urasaapi.com/api/getposts?page="+this.current)
              .then((response) => {
                   console.log(response.data.data);
                  this.posts = response.data.data.data;

              })
              .catch((e) => {
                  this.errors.push(e);
              });
               window.scrollTo(0,0);
          },

      onSubmit(event) {
        event.preventDefault()
        console.log(this.subsemail)
        axios
            .post("https://urasaapi.com/api/getemail", {email :this.subsemail, domain:window.location.hostname })
            .then((response) => {
                 console.log(response.data.message);
                 this.subsmess=response.data.message


            })
            .catch((e) => {
                this.errors.push(e);
            });

      },
      validateEmail(email) {
        if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(subsemail)) {
          this.errorMessage = ''
        } else {
          this.errorMessage = 'Invalid Email'
        }
      },

      watch: {
    subsemail(value){
      this.subsemail = value;
      this.validateEmail(value);
    }
  },


       }
   };

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

        <div class="card  bc1 position-relative" v-for="(post, index) in posts">
             <img class="card-img" :src="post.image" alt="feature-image">
<a :href="'/post/'+post.id" class="text-white text-decoration-none">
            <div class="text-white text-center w-75  p-4 shadow bc2 position-absolute bottom-0 start-50 translate-middle-x">
              <h4>{{post.title}}</h4>
            </div>
            </a>
        </div>

        <div class="d-flex justify-content-between align-items-center mx700px">
            <button  class="btn btn-primary bc1 border-0" @click="prev">Previous</button>
            <button  class="btn btn-primary bc1 border-0" @click="next">Next</button>
        </div>


        </div>
        <div class="col-lg-4 col-md-12 col-sm-12 bi1 position-relative">

           <div class="bg-dark w-100 h-100 position-absolute tint"></div>

            <div class="card subscard my-4 p-4 bg-dark">
               <h5 class="text-center text-white">Subscribe Us</h5>
               <h5 class="text-center text-white text-capitalize">to get latest Updates</h5>

               <form @submit="onSubmit" class="add-form">
               <input v-model="subsemail" placeholder="Enter Email Address" type="email" class="mt-4 ps-4 rounded-pill shadow p-2 border" required>

               <button type="submit" value="Submit" class="btn btn-dark bc1 op rounded-pill mt-2">Subscribe</button>
               <p class="text-danger">{{ errorMessage }}</p>
               <p class="text-success">{{subsmess}}</p>
               </form>



            </div>

            <div class="card text-center subscard my-4 p-4 bg-dark">
               <h5 class="text-center text-white">Follow Us</h5>
               <socialicon color="c1" />

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
  max-width:700px;
  width:100%;
  height:400px;
  margin-bottom:50px;

}
.mx700px{
max-width:700px;
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
