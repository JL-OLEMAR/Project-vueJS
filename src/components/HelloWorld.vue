<template>
  <section id="content">
    <h1 class="subheader">{{ titulo }}</h1>
    <h2>{{ texto }}</h2>
  </section>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      titulo: "Hola Mundo",
      texto: "Hola Mundo desde el componente!!!",
    };
  },
};
</script>
