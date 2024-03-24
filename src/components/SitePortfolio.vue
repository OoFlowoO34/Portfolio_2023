<template>
  <q-layout
    class="card bg-white text-black shadow-10 rounded-border-30 q-mb-xl"
  >
    <div
      class="my-card q-px-xs-md q-px-sm-lg q-px-sm-xl q-py-xs-lg q-py-sm-xl"
      flat
    >
      <div id="group" class="row wrap">
        <div class="left col-12 col-md-7">
          <div
            id="test"
            class="row wrap justify-center q-px-xs-sm q-px-sm-xl"
            style="height: 100%"
          >
            <div class="text col-12">
              <div class="row q-pb-lg">
                <div class="col-auto text-subtitle1 text-weight-bold q-mt-md">
                  <span>{{ title }} </span>
                </div>
                <div class="col-7">
                  <div class="row justify-start" style="height: 100%">
                    <div
                      v-for="(icons, i) in icon"
                      :key="i"
                      class="col-2 col-lg-1 self-center"
                    >
                      <q-item-section v-if="icon[i]" class="q-pa-none" avatar>
                        <q-img
                          :src="require(`../assets/${icon[i]}.png`)"
                          fit="contain"
                          class="self-center rounded-borders"
                          width="24px"
                        />
                        <q-tooltip class="text-body2">{{ icon[i] }}</q-tooltip>
                      </q-item-section>
                    </div>
                  </div>
                </div>
              </div>
              <div class="text-body2">
                <span v-html="text"></span>
              </div>
            </div>
          </div>
        </div>

        <div
          id="img"
          class="right col-12 col-md-5 flex flex-center q-px-xs-sm q-px-sm-xl q-pl-md-lg q-pt-lg"
        >
          <q-img
            :src="require(`../assets/${image}`)"
            fit="cover"
            style="width: 100%"
            class="rounded-borders"
          ></q-img>
        </div>
      </div>

      <div
        id="btn"
        class="button col-12 self-end q-pt-xs-lg q-pl-xs-sm q-pl-sm-xl"
      >
        <div>
          <!-- Condition if/else -->
          <template v-if="link">
            <q-btn
              :href="link"
              target="_blank"
              padding="xs md"
              outline
              color="primary"
              :label="buttonList.button[locale]"
              no-caps
            />
          </template>
          <template v-else>
            <!-- Autre contenu à afficher lorsque la condition est fausse -->
            <q-btn
              disabled
              :href="link"
              target="_blank"
              padding="xs md"
              outline
              color="grey"
              label="Coming soon"
              no-caps
            />
          </template>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import { defineComponent, reactive } from "vue";

export default defineComponent({
  setup() {
    const buttonList = reactive({
      button: {
        FR: "Consulter",
        EN: "Go to the website",
      },
    });
    return {
      buttonList,
    };
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    text: {
      type: Array,
      required: true,
    },
    button: {
      type: Array,
      required: true,
    },
    caption: {
      type: Array,
      required: true,
    },
    icon: {
      type: Array,
      required: true,
    },
    link: {
      type: Array,
      required: true,
    },
    image: {
      type: Array,
      required: true,
    },
    locale: {
      type: String,
      required: true,
    },
  },
  mounted() {
    //this.moveRightElement();
    /**
     * Cette partie peut être enlevé et relayé au css avec du display flex en découpant le composant comme ça plûtot
     * en sortant le bouton de la div "#test"
     *
     * En général, dans un composant vu, il vaut mieux ne pas utiliser document.getElementById pour récupérer un composant mais une ref
     * Car dans ton cas tu instancis 2 fois le composant SitePorfolio et donc dans le DOM, tu les id en double
     *
     * <div ref="maDiv">
     *
     * Dans le js => this.$refs.maDiv    Equiv document.getElementById
     *
     *  __________________________________________
     * |  ___________________    ________________ |
     * | |                   |  |                ||
     * | |      Textes       |  |     image      ||
     * | |___________________|  |________________||
     * |  _______________________________________ |
     * | | BTN                                   ||
     * | |_______________________________________||
     * |__________________________________________|
     */
    // let img = document.getElementById("img");
    // let btn = document.getElementById("btn");
    // let test = document.getElementById("test");
    // let group = document.getElementById("group");
    // console.log(window.innerWidth);
    // window.addEventListener("load", function () {
    //   window.dispatchEvent(new Event("resize"));
    // });
    // window.onresize = function () {
    //   if (window.innerWidth < 1024) {
    //     test.insertBefore(img, btn);
    //   } else {
    //     group.appendChild(img);
    //   }
    // };
  },
  methods: {},
});
</script>

<style scoped></style>
