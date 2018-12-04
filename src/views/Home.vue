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
      message: "PDF Renderer"
    };
  },
  created: function() {},
  methods: {
    createPDF() {
      var doc = new jsPDF();

      doc.text("Photo", 10, 10);
      doc.text("First Name", 10, 20);
      doc.text("Last Name", 10, 20);
      doc.text("Email", 10, 30);
      doc.text("Phone Number", 10, 40);
      doc.text("Short Bio", 50, 100);
      doc.text("Linkedin URL", 10, 200);
      doc.text("Online Resume URL", 10, 200);
      doc.text("Twitter Handle", 10, 200);
      doc.text("Personal Blog/Website URL", 10, 200);
      doc.text("GitHub URL", 10, 200);
      doc.save("a4.pdf");
    }
  },
  computed: {}
};
</script>
