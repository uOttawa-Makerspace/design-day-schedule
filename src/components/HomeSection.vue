<template>
  <section id="home">
    <v-layout :style="cssProps" style="min-height: 600px;" align-center>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="center">
            <v-col cols="12" md="6" xl="8">
              <v-card rounded flat class="pa-5" fill-height>
                <h1 class="display-2 font-weight-bold mb-4">Journée du design hiver 2021</h1>
                <h1 class="display-2 font-weight-bold mb-4">Winter 2021 Design Day</h1>
                <h2>
                  Creativity and ingenuity on display!
                  Design Day promises to amaze you with our students' innovation and inspiration!
                  Students have worked closely with external partners of the Faculty to develop solutions for real clients. This event showcases engineering design projects, and celebrates the achievements of our students.
                </h2>
                <v-btn rounded large dark @click="$vuetify.goTo('#schedule')" class="mt-5">
                  Horaire / Schedule
                  <v-icon class="ml-2">mdi-arrow-down</v-icon>
                </v-btn>
              </v-card>
            </v-col>
            <br>
            <v-col cols="12" md="6" xl="4" class="hidden-sm-and-down"> </v-col>
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
        backgroundImage: `url(${require('@/assets/img/3dprinter.jpg')})`,
        'background-position': 'center'
      }
    }
  }
}
</script>

<style>
.svg-border-waves {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 3rem;
  width: 100%;
  overflow: hidden;
}

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

.card {
  min-height: 300px;
  padding: 10px;
  transition: 0.5s ease-out;
}

.card .v-image {
  margin-bottom: 15px;
  transition: 0.75s;
}

.card h1 {
  margin-bottom: 10px;
}

.zoom-effect {
  transform: scale(1.1);
}

.up {
  transform: translateY(-20px);
  transition: 0.5s ease-out;
}
</style>

<style>
section {
  position: relative;
}
</style>
