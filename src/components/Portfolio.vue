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
          EN: "Project completed during my internship as a Web Developer.<br><br><strong>Features:</strong><ul><li><span style='text-decoration: underline;'>Profile:</span> Registration (email verification), login, username, password, photo, show likes.</li><li><span style='text-decoration: underline;'>Requests:</span> Show requests from other users, adding requests, show own requests, editing own requests, deleting own requests.</li><li><span style='text-decoration: underline;'>Messages:</span> Sending messages to the author of a request, responding to received messages, show inbox, liking other users.</li></ul><br><br><span style='text-decoration: underline;'><strong>Try the website</strong></span> => Email: toto@toto.fr - Password: tototo",
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
          FR: "Projet personnel avec pour objectif de réaliser une nouvelle version de mon portfolio en Vue.js en utilisant Quasar.<br> Sélection de la langue anglais/français dynamique.<br> Utilisation d'une font variable et animation lottie.",
          EN: "Personal project with the objective of creating a new version of my portfolio using Vue.js and Quasar.<br>Use of a variable font and Lottie animations.",
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
      {
        title: {
          FR: "A'Rosa-je",
          EN: "A'Rosa-je",
        },
        text: {
          FR: "Développement d'une application mobile (flutter), de son back office (Vue.js) et de son API (Dot.net).<br>L'application permet à l'utilisateur de faire garder ses plantes par un autre.<br>Des botanistes professionnels peuvent fournir des conseils aux utilisateurs.<br>Projet réalisé lors de mes études à l'epsi en groupe de 4 personnes.<br><br><strong>Compétences:</strong> <br> Maquetter une application.<br> Développer des composants d’accès aux données.<br> Développer la partie Front-End d’une interface utilisateur.<br> Développer la partie Back-End d’une interface utilisateur.<br> Collaborer à la gestion d’un projet informatique et à l’organisation de l’environnement de développement<br> Concevoir une application<br> Construire une application organisée en couches<br> Développer une application mobile<br><ul> Préparer et exécuter le déploiement d’une application<li>Installer et configurer son environnement de travail en fonction du projet</li><li>Contribuer à la mise en production dans une démarche DevOps</li><li>Collaborer à la gestion d'un projet informatique et à l'organisation du développement</li></ul>",
          EN: "Development of a mobile application (Flutter), its back office (Vue.js), and its API (Dot.net).<br>The application allows users to have their plants cared for by another person.<br>Professional botanists can provide advice to users.<br>Project carried out during my studies at epsi in a group of 4 people.<br><br><strong>Skills:</strong> <br>Mock-up an application.<br>Develop data access components.<br>Develop the Front-End part of a user interface.<br>Develop the Back-End part of a user interface.<br>Collaborate on the management of an IT project and the organization of the development environment<br>Design an application<br>Build an application organized in layers<br>Develop a mobile application<br><ul>Prepare and execute the deployment of an application<li>Install and configure your working environment according to the project</li><li>Contribute to production deployment in a DevOps approach</li><li>Collaborate on the management of an IT project and the organization of development</li></ul>",
        },

        caption: [
          "quasar.dev",
          "github.com/quasarframework",
          "chat.quasar.dev",
        ],
        icon: ["Vue-js", "Flutter", "Dotnet", "Docker", "Cypress"],
        link: null,
        image: "Arosaje-BO.gif",
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

      this.titleTranslate = [currentPosition / 70, currentPosition / 100];
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
  animation-name: anim-weight;
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
  letter-spacing: 0.1em;
}
.shadow {
  color: rgba(0, 0, 0, 0.5);
}
</style>
