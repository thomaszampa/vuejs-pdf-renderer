<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="createPDF();">Make pdf</button>
  </div>
</template>

<style></style>

<script>
/* global jsPDF */
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "PDF Renderer",

      student: {},
      firstName: ""
    };
  },
  created: function() {},
  methods: {
    createPDF() {
      //Gets student info from back-end
      axios.get("https://gentle-sierra-69054.herokuapp.com/api/students/1").then(
        function(response) {
          console.log(response.data);
          this.student = response.data;

          var doc = new jsPDF();

          var image =
            "https://media.licdn.com/dms/image/C5603AQHYBsTqfW_6wg/profile-displayphoto-shrink_200_200/0?e=1549497600&v=beta&t=YDIdycW2pXneFpBZpjfS1pOiqVZT_lO3lbO55sEqP_E";

          // 210 width of document
          // With 20 unit margin 170

          doc.addImage(image, "JPEG", 20, 10, 60, 60, "guy", "FAST", 0);
          doc.text("", 30, 10);

          //Header text
          //-------------------------------------
          doc.text(this.student.first_name, 110, 20);
          doc.text(this.student.last_name, 140, 20);
          doc.text(this.student.email + " |", 110, 30);
          doc.text(this.student.phone_number, 140, 30);
          doc.line(20, 75, 189, 75);
          //-------------------------------------

          //Bio
          //-------------------------------------
          var bio = this.student.short_bio;

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
          doc.setFontSize(12);
          doc.text("SKILZ", 50, 85);
          doc.text(this.student.skills[0].skill_name, 50, 95);
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
        }.bind(this)
      );
    }
  },
  computed: {}
};
</script>
