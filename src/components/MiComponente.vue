<template>
  <section id="content">
    <hr />
    <h1 class="subheader">{{ titulo }}</h1>
    <h2>{{ subtitulo }}</h2>
    <hr />

    <h2>Reactividad</h2>
    <input type="text" v-model="nombre" />
    Mi nombre es: <strong>{{ nombre }}</strong>
    <!-- <pre>{{$data}}</pre> -->
    <hr />
    <h2>Directivas condicionales</h2>
    <input type="number" v-model="edad" />
    Mi edad es: <strong>{{ edad }}</strong>
    <br />

    <p class="alert-purple-provisional" v-if="edad && edad >= 65">
      ¡¡ERES DE AVANZADA DE EDAD!!
    </p>

    <p
      class="alert-success-provisional"
      v-else-if="edad && edad >= 18 && edad < 65"
    >
      ¡¡ERES MAYOR DE EDAD!!
    </p>
    <p class="alert-danger-provisional" v-else>¡¡ERES MENOR DE EDAD!!</p>

    <hr />
    <h2>Directivas iterativa</h2>
    <ol>
      <li v-for="pelicula in peliculas" :key="pelicula[0]">
        {{ pelicula }}
      </li>
    </ol>
    <hr />
  </section>
</template>

<script>
export default {
  name: "MiComponente",
  data() {
    return {
      titulo: "Mi Componente",
      subtitulo: "Soy el subtítulo de mi componente",
      nombre: "",
      edad: 18,
      peliculas: [
        "Batman vs Superman",
        "El señor de los anillos",
        "Spiderman",
        "Anabelle",
      ],
    };
  },
};
</script>