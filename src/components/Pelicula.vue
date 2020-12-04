<template>
  <article class="article-item" id="article-template">
    <div class="image-wrap">
      <img
        :src="pelicula.image"
        :alt="pelicula.title"
        :title="pelicula.title"
      />
    </div>

    <h2>{{ pelicula.title }}</h2>
    <a href="/blog" class="leer">Leer más</a>
    <input
      type="button"
      value="Marcar como Favorita"
      @click="pasarFavoritaAlPadre(pelicula)"
    />

    <span
      class="date"
      :class="{
        yeargreen: pelicula.year > 2015,
        yearred: pelicula.year <= 2015,
      }"
    >
      {{ pelicula.year }}
    </span>

    <div class="clearfix"></div>
  </article>
</template>

<script>
export default {
  name: "Pelicula",
  props: ["pelicula"],
  methods: {
    pasarFavoritaAlPadre(pelicula) {
      this.$emit("favorita", pelicula);
    },
  },
};
</script>;