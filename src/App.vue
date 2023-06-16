<template>
  <router-view />
</template>

<script>
import { defineComponent, computed } from "vue";

// La variable locale peut être géré ici
export default defineComponent({
  name: "App",
  data() {
    return {
      locale: "FR",
    };
  },
  provide() {
    return {
      // On fournit la variable à tous les enfants
      // Ils l'a récupèreront avec un inject. voir NavCard.vue
      locale: computed(() => this.locale),
    };
  },
  methods: {
    setLocale(locale) {
      this.locale = locale;
    },
  },
});
</script>

<style>
body {
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, #97a0c9 0%, #e9d0c8 100%);
}
@font-face {
  font-family: "Roboto Flex";
  src: url("../public/fonts/RobotoFlex.woff2") format("woff2-variations");
  font-weight: 400;
  font-style: normal;
  font-variation-settings: "wght" 400, "opsz" 100%;
}
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
a {
  text-decoration: none;
  color: black;
}
</style>
