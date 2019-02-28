<template>
  <div class="recipes-show">

    <!-- Section - Profile Start -->
    <section id="profile" class="bg-gray-dark-2 overflow-hidden py-0">
        <div class="container">
            <div class="row">
                <div class="col-xl-7 col-profile" data-mh="mh-col-profile">
                    <div class="pr-lg-4">
                        <h3 class="font-alt font-w-600 letter-spacing-2 title-extra-large text-uppercase text-white">{{ recipe.title }}</h3>
                        <p class="mt-4 text-large text-white">Chef: {{ recipe.chef }}</p>
                        <span class="bg-base-color mt-4 sep-line-medium-thick"></span>
                        <p class="mt-4 text-gray text-large">Prep Time: {{ recipe.formatted.prep_time }}</p>

                        <div class="row pt-5">
                            <div class="col-md-6">
                                <span class="d-block font-alt letter-spacing-2 text-extra-large text-uppercase text-white">Ingredients:</span>
                                <ul class="list-unstyled mt-2 text-gray text-large">
                                    <li v-for="ingredient in recipe.formatted.ingredients">{{ ingredient }}</li>
                                </ul>
                            </div>
                            <!-- //.col-md-6 -->

                            <div class="col-md-6">
                                <span class="d-block font-alt letter-spacing-2 text-extra-large text-uppercase text-white">Directions:</span>
                                <ol class="mt-2 text-gray text-large">
                                    <li v-for="direction in recipe.formatted.directions">{{ direction }}</li>
                                </ol>
                            </div>
                            <!-- //.col-md-6 -->
                            
                            <div class="col-md-6">
                                <router-link class="btn box-shadow-wide btn-base-color btn-large mt-4 mt-md-5" :to=" '/recipes/' + recipe.id + '/edit' ">Edit</router-link>
                            </div>

                            <div class="col-md-6">
                                <button class="btn box-shadow-wide btn-base-color btn-large mt-4 mt-md-5" v-on:click="destroyRecipe()">Delete</button>
                            </div>
                        </div>
                        <!-- //.row -->
                    </div>
                    <!-- //.pr-lg-4 -->
                </div>
                <!-- //.col-xl-7 -->
                
                <div class="col-xl-5 d-none d-xl-block position-relative" data-mh="mh-col-profile">
                    <img :src="recipe.image_url" alt="" class="img-fluid left-0 position-absolute top-0 w-100"/>
                </div>
                <!-- //.col-xl-5 -->
            </div>
            <!-- //.row -->
        </div>
        <!-- //.container -->
    </section>
    <!-- //Section - Profile End -->
    
  </div>
</template>

<style>
  
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      recipe: {
                id: "",
                title: "",
                chef: "",
                ingredients: "",
                prep_time: "",
                image_url: "",
                formatted:{
                  ingredients: [],
                  directions: [],
                  prep_time: "",
                  created_at: ""}
                }
    };
  },
  created: function() {
    axios.get("/api/recipes/" + this.$route.params.id )
      .then(response => {
        console.log(response.data);
        this.recipe = response.data;
      });
  },
  methods: {
    destroyRecipe: function() {
      axios.delete("/api/recipes/" + this.recipe.id)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        });
    }
  }
}
</script>







