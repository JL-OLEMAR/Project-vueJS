<template>
  <section id="articles-component">
    <div id="articles-list" v-if="articles && articles.length >= 0">
      <article
        class="article-item"
        v-for="article in articles"
        :key="article._id"
      >
        <div class="image-wrap">
          <img
            :src="url + 'get-image/' + article.image"
            :alt="article.title"
            v-if="article.image"
          />
          <img
            src="../assets/images/default.png"
            :alt="article.title"
            v-if="!article.image"
          />
        </div>

        <h2>{{ article.title }}</h2>
        <span class="date">{{ article.date | moment("from", "now") }}</span>
        <a href="#" class="leer">Leer más</a>

        <div class="clearfix"></div>
      </article>
    </div>
    <div v-else-if="articles && articles.length < 1">
      No hay artículos para mostrar.
    </div>
    <div v-else>Cargando...</div>
  </section>
</template>

<script>
import Global from "../Global";

export default {
  name: "Articles",
  data() {
    return {
      url: Global.url,
    };
  },
  props: ["articles"],
};
</script>