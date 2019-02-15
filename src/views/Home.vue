<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>{{ message2 }}</p>
    <div>
      <input v-model="message2">
    </div>
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      message: "Josh is sooooo coool and handsome!",
      message2: "...or is he?"
    };
  },
  created: function() {},
  methods: {}
};
</script>