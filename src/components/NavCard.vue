<template>
  <div class="q-pa-md">
    <q-toolbar class="text-black">
      <a href="https://www.epsi.fr">
        <q-img q-m-lg style="width: 24px" src="../assets/Epsi.png" />
        <span style="font-size: 16px">&nbsp;epsi&nbsp;</span>
        <span style="font-size: 10px"
          >&nbsp;école d'ingénierie informatique</span
        >
      </a>

      <q-space />

      <!-- :model-value="locale" sur le qtabs va dire quel est l'onglet sélectioné
      de base pour ne pas avoir a simuler un click -->
      <q-tabs id="languages" class="" shrink :model-value="locale">
        <q-tab
          v-for="(value, key) in languages"
          :key="key"
          class="language"
          :id="key"
          :name="key"
          :label="value[locale]"
          no-caps
          @click="changeLanguage(key)"
        />
      </q-tabs>
    </q-toolbar>
  </div>
</template>
<script>
import { reactive } from "vue";
import { getCurrentInstance, inject } from "vue";

export default {
  components: {},
  data() {
    return {};
  },
  setup() {
    const instance = getCurrentInstance();
    const locale = inject("locale");
    const languages = reactive({
      FR: {
        FR: "Francais",
        EN: "French",
      },
      EN: {
        FR: "Anglais",
        EN: "English",
      },
    });

    function changeLanguage(lang) {
      instance.root.ctx.setLocale(lang);

      // Voir App.vue

      // Ici la la fonction changeLanguage va faire remonter le changement au premier Composant App.vue

      // La réactivité se fait dans tous les composants ou tu demande la valeur

      // const locale = inject('locale') // FR ou EN
    }

    return {
      languages,
      locale,
      changeLanguage,
    };
  },
  methods: {},
  mounted() {},
};
</script>
<style scoped>
#logo {
  border: solid 1px black;
}
</style>
