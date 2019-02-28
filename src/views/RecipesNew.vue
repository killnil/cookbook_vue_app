<template>
  <div class="recipes-new">
    <!-- Section - Contact Start -->
    <section id="contact" class="bg-gray-dark-2">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-lg-8 text-center">
                    <h3 class="font-alt font-w-600 letter-spacing-2 title-extra-large text-uppercase text-white">New Recipe</h3>
                    <p class="mt-3 text-gray text-extra-large"><i>Make something "delicious"</i></p>
                    <span class="bg-base-color mt-4 mx-auto sep-line-medium-thick-long"></span>
                </div>
                <!-- //.col-lg-8 -->
            </div>
            <!-- //.row -->
            
            
            <div class="row justify-content-center mt-5 pt-lg-5">
                <div class="col-lg-8">
                  <ul>
                    <li class="text-gray" v-for="error in errors">{{ error }}</li>
                  </ul>
                    <form v-on:submit.prevent="submit()" id="form-contact">
                        <div class="row">
                            <div class="col-lg-6">
                                <div class="form-group">
                                    <input type="text" class="font-alt form-control required" id="title" placeholder="Title" v-model="newRecipeTitle">
                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-lg-6 -->

                            
                            <div class="col-lg-6">
                                <div class="form-group">
                                    
                                    <input type="text" class="font-alt form-control required" id="chef" placeholder="Chef" v-model="newRecipeChef">

                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-lg-6 -->

                            <div class="col-lg-6">
                                <div class="form-group">
                                    <input type="text" class="font-alt form-control required" id="prep-time" placeholder="Prep Time" v-model="newRecipePrepTime">
                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-lg-6 -->

                            <div class="col-lg-6">
                                <div class="form-group">
                                    <input type="text" class="font-alt form-control required" id="image-url" placeholder="Image URL" v-model="newRecipeImageUrl">
                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-lg-6 -->
                            
                            <div class="col-12">
                                <div class="form-group">
                                    <textarea class="font-alt form-control required" id="ingredients" rows="12" placeholder="Ingredients" v-model="newRecipeIngredients"></textarea>
                                    
                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-12 -->
                            
                            <div class="col-12">
                                <div class="form-group">
                                    <textarea class="font-alt form-control required" id="directions" rows="12" placeholder="Directions" v-model="newRecipeDirections"></textarea>
                                </div>
                                <!-- //.form-group -->
                            </div>
                            <!-- //.col-12 -->
                            
                            <div class="col-12">
                                <span class="d-block font-alt letter-spacing-1 text-gray text-small text-uppercase">*Please make sure all recipes are eatable</span>
                                <button type="submit" class="btn btn-base-color btn-block btn-large box-shadow-wide mt-5 mx-0 text-white" id="btn-form-contact">Create Recipe</button>
                            </div>
                            <!-- //.col-12 -->
                        </div>
                        <!-- //.row -->
                    </form>
                </div>
                <!-- //.col-lg-8 -->
            </div>
            <!-- //.row -->
        </div>
        <!-- //.container -->
    </section>
    <!-- //Section - Contact End -->
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      newRecipeTitle: "",
      newRecipeChef: "",
      newRecipePrepTime: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipeImageUrl: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    submit: function() {
      console.log("Create the Recipe...");
      var params = {
                    title: this.newRecipeTitle,
                    chef: this.newRecipeChef,
                    prep_time: this.newRecipePrepTime,
                    ingredients: this.newRecipeIngredients,
                    directions: this.newRecipeDirections,
                    image_url: this.newRecipeImageUrl
                    };
      axios.post("/api/recipes", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>










