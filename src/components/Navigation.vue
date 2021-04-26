<template>
  <div>
    <v-navigation-drawer v-model="drawer" app temporary>
      <v-list>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title">Journée du design hiver 2021</v-list-item-title>
            <v-list-item-title class="title">Winter 2021 Design Day</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <v-divider />

      <v-list>
        <v-list-item v-for="([icon, text, link], i) in items" :key="i" link @click="$vuetify.goTo(link)">
          <v-list-item-icon class="justify-center">
            <v-icon>{{ icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title class="subtitle-1">
              {{ text }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app id="header">
      <v-toolbar-title>
        <span class="mr-2">Journée du design hiver 2021 / Winter 2021 Design Day</span>
      </v-toolbar-title>
      <v-spacer />
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" class="mr-4" v-if="isXs"/>
      <div v-else>
        <v-btn text @click="$vuetify.goTo('#home')">
          <span class="mr-2">Accueil / Home</span>
        </v-btn>
        <v-btn rounded outlined text @click="$vuetify.goTo('#schedule')">
          <span class="mr-2">Horaire / Schedule</span>
        </v-btn>
        <v-btn rounded outlined text @click="$vuetify.goTo('#presentations')">
          <span class="mr-2">Presentations</span>
        </v-btn>
        <v-btn rounded outlined text @click="$vuetify.goTo('#sponsors')">
          <span class="mr-2">Partenaires / Sponsors</span>
        </v-btn>
        <v-btn rounded outlined text @click="$vuetify.goTo('#recordings')">
          <span class="mr-2">Enregistrements / Recordings</span>
        </v-btn>
      </div>
    </v-app-bar>
  </div>
</template>

<style scoped>
.v-toolbar {
  transition: 0.6s;
}
</style>

<script>
export default {
  data: () => ({
    drawer: null,
    isXs: false,
    items: [
      ["mdi-home-outline", "Accueil / Home", "#home"],
      ["mdi-information-outline", "Horaire / Schedule", "#schedule"],
      ["mdi-information-outline", "Presentations", "#presentations"],
      ["mdi-email-outline", "Partenaires / Sponsors", "#sponsors"],
      ["mdi-information-outline", "Enregistrements / Recordings", "#recordings"],
    ],
  }),
  props: {
    color: String,
  },
  methods: {
    onResize() {
      this.isXs = window.innerWidth < 1220;
    },
  },

  watch: {
    isXs(value) {
      if (!value) {
        if (this.drawer) {
          this.drawer = false;
        }
      }
    },
  },
  mounted() {
    this.onResize();
    window.addEventListener("resize", this.onResize, { passive: true });
  },
};
</script>
