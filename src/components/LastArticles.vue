<template>
  <div class="general">
    <Slider texto="Bienvenido al Curso de Vue" home="true"></Slider>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Últimos artículos</h2>

        <!--Listado últimos 5 artículos-->
        <div id="articles">
          <Articles v-bind:articles="articles"></Articles>
        </div>

      </section>
      <Sidebar></Sidebar>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Global from "../Global";
import Slider from "./Slider.vue";
import Sidebar from "./Sidebar.vue";
import Articles from "./Articles.vue";

export default {
  name: "LastArticles",
  components: {
    Slider,
    Sidebar,
    Articles,
  },
  data() {
    return {
      url: Global.url,
      articles: null,
    };
  },
  mounted() {
    this.getLastArticles();
  },
  methods: {
    getLastArticles() {
      axios.get(this.url + "articles/true").then((res) => {
        if (res.data.status == "success") {
          this.articles = res.data.articles;
          console.log(this.articles);
        }
      });
    },
  },
};
</script>