<template src="./CreateArticle.html"></template>

<script>
import Sidebar from "./Sidebar.vue";
import Global from "../Global";
import Article from "../models/Article";
import axios from "axios";
import { required } from "vuelidate/lib/validators";
import swal from "sweetalert";

export default {
  name: "EditArticle",
  components: {
    Sidebar,
  },
  data() {
    return {
      url: Global.url,
      file: "",
      article: new Article("", "", null, ""),
      submitted: false,
      isEdit: true,
    };
  },
  mounted() {
    var articleId = this.$route.params.id;
    this.getArticle(articleId);
  },
  validations: {
    article: {
      title: {
        required,
      },
      content: {
        required,
      },
    },
  },
  methods: {
    fileChange() {
      this.file = this.$refs.file.files[0];
      console.log(this.file);
    },
    save() {
      this.submitted = true;
      var articleId = this.$route.params.id;
      this.$v.$touch();

      if (this.$v.$invalid) {
        return false;
      } else {
        axios
          .put(this.url + "article/" + articleId, this.article)
          .then((response) => {
            if (response.data.status == "success") {
              // Subida de archivo
              if (this.file != null && this.file != undefined && this.file != "") {
                const formData = new FormData();
                formData.append("file0", this.file, this.file.name);

                var articleId = response.data.articleUpdated._id;
                axios
                  .post(this.url + "upload-image/" + articleId, formData)
                  .then((response) => {
                    if (response.data.article) {
                      swal(
                        "Artículo actualizado",
                        "El artículo se ha actualizado correctamente :)",
                        "success"
                      );

                      this.article = response.data.article;
                      this.$router.push("/articulo/" + this.article._id);
                    } else {
                      //  Mostrar alerta de error
                      swal(
                        "Artículo fallido",
                        "El artículo NO se ha actualizado",
                        "error"
                      );
                    }
                  })
                  .catch((error) => {
                    console.log(error);
                  });
              } else {
                swal(
                  "Artículo actualizado",
                  "El artículo se ha actualizado correctamente :)",
                  "success"
                );
                this.article = response.data.articleUpdated;
                this.$router.push("/articulo/" + this.article._id);
              }
            }
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
    getArticle(articleId) {
      axios.get(this.url + "article/" + articleId).then((res) => {
        if (res.data.status == "success") {
          this.article = res.data.article;
        }
      });
    },
  },
};
</script>
