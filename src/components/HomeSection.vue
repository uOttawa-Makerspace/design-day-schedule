<template>
  <section id="home">
    <v-layout :style="cssProps" style="min-height: 650px;" align-center>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="center">
            <v-col cols="12" md="6" xl="8">
              <v-card rounded flat class="pa-5" fill-height>
                <h1 class="display-2 font-weight-bold mb-4">Journée du design hiver 2022</h1>
                <h1 class="display-2 font-weight-bold mb-4">Winter 2022 Design Day</h1>
                <h3>
                  Ingéniosité et créativité en valeur!
                  La Journée du design saura vous épater par notre innovation et inspiration étudiante!
                  En collaboration avec des partenaires de l'industrie et de la communauté, nos étudiants ont développé
                  des solutions concrètes pour leurs clients. Cet événement offre l'opportunité aux étudiants de
                  présenter leurs projets de conception, de célébrer leur réussite et de gagner des prix.
                </h3>
                <br>
                <h3>
                  Creativity and ingenuity on display!
                  Design Day promises to amaze you with our students' innovation and inspiration!
                  Students have worked closely with external partners of the Faculty to develop solutions for real
                  clients. This event showcases engineering design projects, and celebrates the achievements of our
                  students.
                </h3>
                <v-btn rounded large dark @click="$vuetify.goTo('#schedule')" class="mt-5">
                  Horaire / Schedule
                  <v-icon class="ml-2">mdi-arrow-down</v-icon>
                </v-btn>
              </v-card>
            </v-col>
            <br>
            <v-col cols="12" md="6" xl="4" class="hidden-sm-and-down"></v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-layout>
  </section>
</template>

<script>
export default {
  data() {
    return {
      cssProps: {
        backgroundImage: `url(${require('@/assets/img/awardpicture.jpg')})`,
        'background-position': 'center'
      }
    }
  }
}
</script>

<style>
#home {
  z-index: 0;
}

.svg-border-waves img {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  margin-bottom: -2px;
  z-index: -1;
}

.card .v-image {
  margin-bottom: 15px;
  transition: 0.75s;
}

.card h1 {
  margin-bottom: 10px;
}

</style>

<style>
section {
  position: relative;
}
</style>
