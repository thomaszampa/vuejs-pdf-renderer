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

      var image =
        "https://media.licdn.com/dms/image/C5603AQHYBsTqfW_6wg/profile-displayphoto-shrink_200_200/0?e=1549497600&v=beta&t=YDIdycW2pXneFpBZpjfS1pOiqVZT_lO3lbO55sEqP_E";

      // 210 width of document
      // With 20 unit margin 170

      doc.addImage(image, "JPEG", 20, 10, 60, 60, "guy", "FAST", 0);
      doc.text("ref", 30, 10);

      //Header text
      //-------------------------------------
      doc.text("First Name", 110, 20);
      doc.text("Last Name", 140, 20);
      doc.text("Email" + " |", 110, 30);
      doc.text("Phone Number", 140, 30);
      doc.line(20, 75, 189, 75);
      //-------------------------------------

      //Bio
      //-------------------------------------
      var bio =
        "From studios and start-ups in Nashville to post-production houses in Chicago, my professional career has evolved beyond any initial expectations I had leaving Belmont University with a degree in business administration. Nashvilles exploding economy gave me the hunger and drive to get involved with cutting-edge companies shaking up the music industry. Utilizing new technologies and unconventional growth strategies, I was able to create opportunities for my artists and the company as a whole.";

      var splitBio = doc.splitTextToSize(bio, 160);

      doc.setFontSize(10);
      doc.text(splitBio, 90, 40);
      //-------------------------------------

      //Education
      //-------------------------------------
      doc.setFontSize(12);
      doc.text("EDUCATION", 10, 85);

      //-------------------------------------

      // //Experience
      // //-------------------------------------
      // doc.setFontSize(12);
      // doc.text("EDUCATION", 10, 85);
      // //-------------------------------------

      // //Skills
      // //-------------------------------------
      // doc.setFontSize(12);
      // doc.text("EDUCATION", 10, 85);
      // //-------------------------------------

      // //Capstone
      // //-------------------------------------
      // doc.setFontSize(12);
      // doc.text("EDUCATION", 10, 85);
      // //-------------------------------------

      //Footer
      //-------------------------------------
      doc.setFontSize(8);
      doc.setTextColor(0, 102, 204);
      doc.line(20, 285, 189, 285);
      doc.textWithLink("Linkedin URL", 20, 290, { url: "https://www.linkedin.com/in/kevinnagel/" });
      doc.textWithLink("Online Resume URL", 50, 290, { url: "https://www.linkedin.com/in/kevinnagel/" });
      doc.textWithLink("Twitter Handle", 88, 290, { url: "https://www.linkedin.com/in/kevinnagel/" });
      doc.textWithLink("Personal Blog/Website URL", 120, 290, { url: "https://www.linkedin.com/in/kevinnagel/" });
      doc.textWithLink("GitHub URL", 170, 290, { url: "https://www.linkedin.com/in/kevinnagel/" });
      //-------------------------------------

      //Download PDF
      doc.save("a4.pdf");
    }
  },
  computed: {}
};
</script>
