<template>
  <div id="talk" class="q-pa-xs-sm q-pa-md-lg">
    <q-layout class="card bg-white text-black shadow-10 rounded-border-30">
      <div class="q-px-xs-md q-px-sm-lg q-px-sm-xl q-py-xs-sm q-py-sm-md" flat>
        <div
          class="row reverse-wrap q-px-xs-sm q-px-sm-xl q-py-xs-sm q-py-sm-md"
        >
          <div class="col-12 col-sm-7">
            <h2 v-show="locale == 'FR'" class="text-boldn q-mt-none q-my-sm-xl">
              Me contacter
            </h2>
            <h2 v-show="locale == 'EN'" class="text-boldn q-mt-none q-my-sm-xl">
              Let's talk !
            </h2>

            <div class="row" style="">
              <div
                v-for="(link, i) in linksList"
                :key="i"
                class="col-12 col-md-6"
              >
                <a
                  class="row no-wrap q-pt-md"
                  :href="link.link"
                  target="_blank"
                  style="width: fit-content"
                >
                  <q-icon :name="link.icon" size="md" class="text-primary" />

                  <span
                    :id="link.icon"
                    class="wave-word col-auto self-center q-pa-sm"
                  >
                    <span
                      :class="link.icon + '-letter'"
                      v-for="(char, index) in link.title.split('')"
                      :key="index"
                      >{{ char }}</span
                    ></span
                  >
                </a>
              </div>
            </div>
          </div>

          <div class="col-12 col-sm-5 flex flex-center q-py-lg">
            <q-avatar style="height: 200px">
              <Vue3Lottie
                class="vue3-lottie"
                :animationData="ContactJSON"
                :height="200"
                :width="200"
                :speed="0.25"
                style="
                  position: absolute;
                  top: 50%;
                  left: 50%;
                  transform: translate(-50%, -50%);
                "
              />
            </q-avatar>
          </div>
        </div>

        <div
          class="row justify-between q-gutter-md q-pa-xs-sm q-pa-sm-xl q-py-xs-xl"
        >
          <q-btn
            :href="cvUrl"
            download="CV-Florian-Batt.pdf"
            class="col-5"
            padding="md xl"
            color="primary"
            :label="buttonList.button[locale]"
            icon="download"
            no-caps
          />
        </div>
      </div>
    </q-layout>
  </div>
</template>

<script>
import cv from "../assets/CV_Florian_Batt_2024.pdf";
import portfolio from "../assets/portfolio.pdf";
import { defineComponent, inject } from "vue";
import { reactive } from "vue";
import { Vue3Lottie } from "vue3-lottie";
import "vue3-lottie/dist/style.css";

import ContactJSON from "../assets/Lottie-contact.json";

export default defineComponent({
  name: "TheContact",
  components: {
    Vue3Lottie,
  },
  data() {
    return {
      ContactJSON,
    };
  },
  setup() {
    const locale = inject("locale");
    const linksList = reactive([
      {
        title: "06474142934",
        icon: "phone",
        link: "tel:+330674142934",
      },
      {
        title: "florian.batt@hotmail.fr",
        icon: "mail",
        link: "mailto:florian.batt@hotmail.fr",
      },
    ]);
    const buttonList = reactive({
      button: {
        FR: "Télécharger mon CV",
        EN: "Download my CV",
      },
    });

    return {
      linksList,
      cvUrl: cv,
      portfolioUrl: portfolio,
      buttonList,
      locale,
    };
  },
  props: {
    receivedVariable: {
      type: String,
      required: true,
    },
  },
  mounted() {
    const phoneEl = document.querySelector("#phone");
    const mailEl = document.querySelector("#mail");

    phoneEl.addEventListener("mouseenter", function () {
      wave.call(this);
    });
    mailEl.addEventListener("mouseenter", function () {
      wave.call(this);
    });

    setInterval(wave.bind(phoneEl), 5000);
    setTimeout(() => {
      setInterval(wave.bind(mailEl), 5000);
    }, 1000);

    function wave() {
      Array.from(this.childNodes)
        .filter((node) => node.nodeType === Node.ELEMENT_NODE)
        .forEach((element, index) => {
          setTimeout(() => {
            element.classList.add("wave");
          }, index * 50);
        });
      Array.from(this.childNodes)
        .filter((node) => node.nodeType === Node.ELEMENT_NODE)
        .forEach((node) => {
          if (node.classList.contains("wave")) {
            node.classList.remove("wave");
          }
        });
    }

    // letters.forEach((WordArray) => {
    //   WordArray.addEventListener("click", () => {
    //     changeSizeOnClick(letters);
    //   });
    // });
    // function changeSizeOnClick(letters) {
    //   const fontSize = 14;
    //   const fontSizeMax = 24;
    //   const step = 1;
    //   let currentFontSize = fontSize;
    //   let isIncreasing = true;
    //   const intervalId = setInterval(() => {
    //     if (isIncreasing) {
    //       if (currentFontSize >= fontSizeMax) {
    //         isIncreasing = false;
    //       } else {
    //         currentFontSize += step;
    //       }
    //     } else {
    //       if (currentFontSize <= fontSize) {
    //         clearInterval(intervalId);
    //       } else {
    //         currentFontSize -= step;
    //       }
    //     }
    //     letters.forEach((letter, index) => {
    //       setTimeout(() => {
    //         letter.style.fontSize = `${currentFontSize}px`;
    //       }, index * 500);
    //     });
    //   }, 1000 / (fontSizeMax - fontSize));
    // }
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
#word {
  font-family: "Roboto Flex";
  font-size: 40px;
  display: inline-block;
}

.wave {
  font-family: "Roboto Flex";

  display: inline-block;
  animation-name: varfont;
  animation-duration: 1s;

  animation-iteration-count: 1;
}

.wave-word {
  font-family: "Roboto Flex";
  font-size: 14px;
  font-weight: 400;
  font-variation-settings: "YTLC" 570, "YTAS" 854, "YTDE" -98, "YTUC" 760,
    "YTFI" 788, "wght" 400;
}

.source-sans-variable {
  font-family: "Roboto Flex", sans-serif;
  font-variation-settings: "wght" 400;
}

.source-sans-variable:hover {
  font-variation-settings: "wght" 900;
}

@keyframes varfont {
  0% {
    font-weight: 400;
    font-variation-settings: "YTLC" 570, "YTAS" 854, "YTDE" -98, "YTUC" 760,
      "YTFI" 788, "wght" 400;
  }

  50% {
    font-weight: 400;
    font-variation-settings: "YTLC" 416, "YTAS" 649, "YTDE" -305, "YTUC" 528,
      "YTFI" 560, "wght" 400;
  }
  100% {
    font-weight: 400;
    font-variation-settings: "YTLC" 570, "YTAS" 854, "YTDE" -98, "YTUC" 760,
      "YTFI" 788, "wght" 400;
  }
}
</style>
