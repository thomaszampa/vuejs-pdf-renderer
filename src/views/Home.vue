<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createPDF();">Make pdf</button>
  </div>
</template>

<style></style>

<script>
/* global jsPDF */

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!"
    };
  },
  created: function() {},
  methods: {
    createPDF() {
      var doc = new jsPDF();

      doc.text("Hello world!", 10, 10);
      doc.save("a4.pdf");
    }
  },
  computed: {}
};
</script>
