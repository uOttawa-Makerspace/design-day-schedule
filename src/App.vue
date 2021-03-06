<template>
  <v-app>
    <navigation />
    <v-main class="pt-0">
      <home ref="home" :style="hheight" />
      <ScheduleSection :zoom_link="zoom_link" />
      <PresentationsSection :zoom_link="zoom_link" />
      <SponsorSection />
    </v-main>
    <v-scale-transition>
      <v-btn fab v-show="fab" v-scroll="onScroll" dark fixed bottom right color="secondary" @click="toTop">
        <v-icon>mdi-arrow-up</v-icon>
      </v-btn>
    </v-scale-transition>
    <bottom_nav />
  </v-app>
</template>

<style scoped>
.v-main {
  background-image: url("~@/assets/img/bgMain.png");
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}
</style>

<script>
import navigation from "./components/Navigation";
import footer from "./components/Footer";
import ScheduleSection from "./components/ScheduleSection";
import home from "./components/HomeSection";
import schedule from "./components/ScheduleSection";
import SponsorSection from "@/components/SponsorSection";
import PresentationsSection from "@/components/PresentationsSection";

export default {
  name: "App",

  components: {
    ScheduleSection,
    PresentationsSection,
    SponsorSection,
    navigation,
    schedule,
    bottom_nav: footer,
    home,
  },

  data: () => ({
    zoom_link: 'TBD',
    fab: null,
    hheight: 'padding-top: 0px;',
    flat: null,
  }),

  created() {
    const top = window.pageYOffset || 0;
    if (top <= 60) {
      this.color = "transparent";
      this.flat = true;
    }
  },

  watch: {
    fab(value) {
      if (value) {
        this.color = "secondary";
        this.flat = false;
      } else {
        this.color = "transparent";
        this.flat = true;
      }
    },
  },

  methods: {
    onScroll(e) {
      if (typeof window === "undefined") return;
      const top = window.pageYOffset || e.target.scrollTop || 0;
      this.fab = top > 60;
    },
    toTop() {
      this.$vuetify.goTo(0);
    },
    onResize() {
      console.log(document.getElementById("header").offsetHeight);
      this.hheight = 'padding-top: '+document.getElementById("header").offsetHeight + "px;";
    },
  },
  mounted() {
    this.onResize();
    window.addEventListener("resize", this.onResize, { passive: true });
  },
};
</script>
