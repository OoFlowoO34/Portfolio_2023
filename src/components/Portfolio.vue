<template>
  <h2
    id="portfolio"
    ref="title"
    class="text-h1 row justify-center relative-position"
    style="font-family: 'RobotoFlex', sans-serif"
  >
    <span
      class="block shadow absolute"
      :style="{
        // transform: `translate(-${titleTranslate[0]}px,-${titleTranslate[1]}px)`,
        zIndex: 1,
        filter: `blur(${titleTranslate[1]}px)`,
      }"
    >
      <span
        v-for="(letter, id) in 'portfolio'.split('')"
        :key="id"
        :style="{ zIndex: id + 1 }"
        >{{ letter }}</span
      >
    </span>
    <span
      class="block absolute"
      :style="{
        transform: `translate(${titleTranslate[0] + 1}px,${
          titleTranslate[1] + 1
        }px)`,
        zIndex: 1,
      }"
    >
      <span
        v-for="(letter, id) in 'portfolio'.split('')"
        :key="id"
        :style="{ zIndex: id + 2 }"
        >{{ letter }}</span
      >
    </span>
    <span class="block invisible non-selectable">
      <span v-for="(letter, id) in 'portfolio'.split('')" :key="id">{{
        letter
      }}</span>
    </span>
  </h2>

  <div class="q-pa-xs-md q-pa-md-xl">
    <SitePortfolio
      :locale="locale"
      v-for="(links, index) in linksList"
      :key="index"
      :title="links.title[locale]"
      :text="links.text[locale]"
      :caption="links.caption"
      :icon="links.icon"
      :link="links.link"
      :image="links.image"
    />
  </div>
</template>

<script>
import { defineComponent, defineProps, reactive, inject } from "vue";
import SitePortfolio from "src/components/SitePortfolio.vue";

export default defineComponent({
  name: "ThePortfolio",
  components: {
    SitePortfolio,
  },
  setup() {
    const locale = inject("locale");
    const linksList = reactive([
      {
        title: {
          FR: "Plate-forme de mise en relation",
          EN: "Linking Platform",
        },
        text: {
          FR: "Projet réalisé pendant mon stage pour l'obtention de mon titre de Développeur Web et Web Mobile. <br><br> <strong>Fonctionnalités:</strong> <ul><li><span style='text-decoration: underline;'>Profil</span>: Inscription (vérification par e-mail), connexion, pseudo, mot de passe, photo, consultation de ses likes.</li> <li><span style='text-decoration: underline;'>Demandes</span>: Consultation des demandes des autres utilisateurs, ajout de demandes, consultation de ses demandes, edition de ses demandes, suppression de ses demandes.</li><li> <span style='text-decoration: underline;'>Messages</span>:  Envoie de messages à l'auteur d'une demande, réponse à un message reçu, consultation de sa messagerie, like d'autres utilisateurs.</li></ul><br><br><span style='text-decoration: underline;'><strong>Pour tester le site</strong></span> => Email: toto@toto.fr - Mdp: tototo",
          EN: "This project is a linking platform to link with your neighboorhood, you can <strong>post</strong> and <strong>share</strong> share stuff, like other users and send <strong>messages</strong>.I made this project during my internship and got my DWWM degree presenting this website. The time to deliver beeing limited I used bootstrap for the style. I particulary enjoyed using Symfony 6, using the bundles and composants such as mailer, rate limiter. It also was really helpfull while dealing with unit tests.",
        },
        caption: [
          "quasar.dev",
          "github.com/quasarframework",
          "chat.quasar.dev",
        ],
        icon: ["Symfony", "php", "JavaScript", "Bootstrap"],
        link: "https://ask.florian-dev.com",
        image: "ask.png",
      },
      {
        title: {
          FR: "Portfolio",
          EN: "Portfolio",
        },
        text: {
          FR: "Projet personnel avec pour objectif de réaliser une nouvelle version de mon portfolio en Vue.js en utilisant Quasar.<br> Utilisation d'une font variable et animation lottie.",
          EN: "This project is a personal portfolio...",
        },
        caption: [
          "quasar.dev",
          "github.com/quasarframework",
          "chat.quasar.dev",
        ],
        icon: ["Vue-js", "Quasar", "JavaScript"],
        link: "https://portfolio.florian-dev.com/",
        image: "portfolio.png",
      },
    ]);

    return {
      linksList,
      locale,
    };
  },
  props: defineProps({
    linksList: {
      type: Array,
      required: true,
    },
  }),
  props: {
    receivedVariable: {
      type: String,
      required: true,
    },
  },
  methods: {
    updateTranslate() {
      // Récupère l'élément que l'on souhaite suivre
      const titleH2 = this.$refs.title;
      if (!titleH2) return;

      // Récupère la position de l'élément
      const elementPosition =
        titleH2.getBoundingClientRect().top + window.scrollY;

      // Calcule la position actuelle de l'élément par rapport au scroll
      const currentPosition = Math.max(
        0,
        elementPosition - window.scrollY - 260
      );

      this.titleTranslate = [currentPosition / 5, currentPosition / 10];
    },
  },
  data() {
    return {
      scrollListener: null,
      titleTranslate: [30, 15],
    };
  },
  unmounted() {
    if (this.scrollListener) window.removeEventListener(this.scrollListener);
  },
  mounted() {
    // Ajoute un événement de scroll sur la fenêtre
    window.addEventListener("load", () => {
      this.updateTranslate();
    });

    // Ajoute un événement de scroll sur la fenêtre
    this.scrollListener = window.addEventListener("scroll", () => {
      this.updateTranslate();
    });
  },
});
</script>
<style scoped>
.rounded-border-30 {
  border-radius: 30px;
}
.card {
  background-size: 80%;
  min-height: fit-content !important;
}

h2 {
  animation-duration: 3s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  animation-name: anim-weiht;
}
@keyframes anim-weight {
  0% {
    font-weight: 400;
  }
  100% {
    font-weight: 500;
  }
  0% {
    font-weight: 400;
  }
}
#portfolio {
  font-size: 5em;
  color: rgba(255, 255, 255);
  margin-top: 16px;
  margin-bottom: 8px;
  letter-spacing: 0.3em;
}
.shadow {
  color: rgba(0, 0, 0, 0.5);
}
</style>
