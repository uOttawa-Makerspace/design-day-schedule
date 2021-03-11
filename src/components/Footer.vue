<template>
  <v-footer dark padless>
    <v-card flat tile class="secondary white--text text-center">
      <v-card-text>
        <v-btn v-for="(icon, i) in icons" :key="i" class="mx-4 white--text" :href="icon.link" target="_blank" icon :alt="icon.alt">
          <v-icon size="24px">{{ icon.text }}</v-icon>
        </v-btn>
      </v-card-text>

      <v-card-text class="white--text">
       &copy {{ new Date().getFullYear() }} — <a class="white--text" href="https://engineering.uottawa.ca/CEED">CENTRE FOR ENTREPRENEURSHIP AND ENGINEERING DESIGN</a> AND
        <a class="white--text" href="https://github.com/uOttawa-Makerspace/design-day-schedule/graphs/contributors">GITHUB CONTRIBUTORS</a>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<style scoped>
.v-card {
  width: 100%;
}
</style>

<script>
export default {
  name: 'Footer',
  data: () => ({
    icons: [
      {
        text: "mdi-facebook",
        link: "https://www.facebook.com/uOCEED/",
        alt: "Facebook Logo"
      },
      {
        text: "mdi-twitter",
        link: "https://twitter.com/uOCEED",
        alt: "Twitter Logo"
      },
      {
        text: "mdi-instagram",
        link: "https://www.instagram.com/uoceed/",
        alt: "Instagram Logo"
      },
    ],
  }),
};
</script>
