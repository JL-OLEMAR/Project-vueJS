<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h1 class="subheader">Películas</h1>

        <!--Mis Datos Computados-->
        <div class="mis-datos" v-if="misDatos">
          <hr />
          <h3>Propiedades Computadas:</h3>
          <p v-html="misDatos"></p>
          <br />
          <h3>Filtros Propios:</h3>
          {{ web | mayusculas | concatenaYear("Este es el mejor año") }}
          <hr />
        </div>

        <!--Pelicula favorita-->
        <div class="favorita" v-if="favorita">
          <hr />
          La película marcada como favorita es:
          <h3>{{ favorita.title }}</h3>
          <hr />
        </div>

        <!--Listado articulos-->
        <div id="articles">
          <div
            v-for="pelicula in peliculasMayuscula"
            v-bind:key="pelicula.title"
          >
            <Pelicula
              :pelicula="pelicula"
              v-on:favorita="haLlegadoLaPeliculaFavorita"
            ></Pelicula>
          </div>
        </div>
      </section>
      <Sidebar></Sidebar>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import Sidebar from "./Sidebar.vue";
import Pelicula from "./Pelicula.vue";

export default {
  name: "Peliculas",
  components: {
    Pelicula,
    Sidebar,
  },
  methods: {
    haLlegadoLaPeliculaFavorita(favorita) {
      this.favorita = favorita;
    },
  },
  filters: {
    mayusculas(value) {
      return value.toUpperCase();
    },
    concatenaYear(value, message) {
      var date = new Date();
      return value + " " + date.getFullYear() + " " + message;
    },
  },
  computed: {
    peliculasMayuscula() {
      var peliculasMod = this.peliculas;
      for (var i = 0; i < this.peliculas.length; i++) {
        peliculasMod[i].title = peliculasMod[i].title.toUpperCase();
      }
      return peliculasMod;
    },
    misDatos() {
      return (
        "<strong>Nombre Completo:</strong> " +
        this.nombre +
        " " +
        this.apellidos +
        "<br/>" +
        "<strong>Sitio web:</strong> " +
        this.web
      );
    },
  },
  data() {
    return {
      nombre: "José",
      apellidos: "Olemar",
      web: "https://github.com/JL-OLEMAR",
      favorita: null,
      peliculas: [
        {
          title: "Batman vs Superman",
          year: 2017,
          image:
            "https://www.lavanguardia.com/r/GODO/LV/p7/WebSite/2020/05/18/Recortada/img_jdelriov_20200518-154128_imagenes_lv_terceros_13321707_511307249069860_6496714579640500048_n-456-k3vD-U481252852604gpE-992x558@LaVanguardia-Web.jpg",
        },
        {
          title: "Fast & Furios 9",
          year: 2015,
          image:
            "https://static.misionesonline.news/wp-content/uploads/2020/03/16084200/rapidos-y-furiosos-9-coronavirus.jpeg",
        },
        {
          title: "Fast & Furios 3",
          year: 2010,
          image:
            "https://static.misionesonline.news/wp-content/uploads/2020/03/16084200/rapidos-y-furiosos-9-coronavirus.jpeg",
        },
        {
          title: "Bumblebee",
          year: 2018,
          image: "https://i.blogs.es/f6cbc7/cartel-bumblebee/450_1000.jpg",
        },
      ],
    };
  },
};
</script>