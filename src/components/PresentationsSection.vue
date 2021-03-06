<template>
  <section class="pb-8" id="presentations">
    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row justify="center">
            <v-col  cols="12" md="7">
              <h1 class="font-weight-light display-2">TBD - Schedule from Spreadsheet</h1>
              <v-simple-table>
                <thead>
                <tr>
                  <th>Nom de la categorie / Category Name</th>
                  <th>Description du projet / Project Description</th>
                  <th>Lien Zoom / Zoom Link</th>
                </tr>
                </thead>
                <tbody>

                <tr v-for="category in categories" v-bind:key="name" >
                  <td>{{category.name}}</td>
                  <td>{{category.gender}}</td>
                  <td>{{category.age}}</td>
                </tr>

                <div v-if="loadingSchedule">Loading schedule - please stand by...</div>

                </tbody>
              </v-simple-table>
              <v-simple-table>
                <thead>
                <tr>
                  <th>Breakout Room</th>
                  <th>Groupe / Groupe</th>
                  <th>Heure / Time</th>
                  <th>Répertoire de projet / Project repository</th>
                </tr>
                </thead>
                <tbody>

                <tr v-for="category in categories" v-bind:key="name" >
                  <td>{{category.name}}</td>
                  <td>{{category.gender}}</td>
                  <td>{{category.age}}</td>
                </tr>

                <div v-if="loadingSchedule">Loading schedule - please stand by...</div>

                </tbody>
              </v-simple-table>

              <br><br>

              <p class="text-justify">
                Rejoignez-nous dans l'appel zoom principal pour la cérémonie de remise des prix et les remarques de clôture à 14h avec ce lien :  <a :href="zoom_link">{{ zoom_link }}</a>
              </p>
              <p class="text-justify">
                Vous pouvez trouver une liste des gagnants <a href="https://genie.uottawa.ca/cgec/concours-etudiant/journee-du-design" alt="Site pour la journée du design">ici</a>.
              </p>

              <p class="text-justify">
                Please join us back in the main zoom call for the award ceremony and closing remarks at 14h with this link :
                <a :href="zoom_link">{{ zoom_link }}</a>
              </p>

              <p class="text-justify">
                You can find the list of winners <a href="https://engineering.uottawa.ca/ceed/student-competitions/design-day" alt="Design Day Website">here</a>.
              </p>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <div class="svg-border-waves text-white">
      <v-img src="~@/assets/img/wave2.svg"/>
    </div>
  </section>
</template>

<style scoped>
.svg-border-waves .v-image {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 3rem;
  width: 100%;
  overflow: hidden;
}

</style>

<script>
export default {
  name: 'PresentationsSection',
  data: () => ({
    categories: [],
    loadingSchedule: true,
    sheetURL: ""
  }),
  props: ['zoom_link'],
  created() {
    this.$papa.parse(this.sheetURL, {
      download: true,
      header: true,
      skipEmptyLines: 'greedy',
      transformHeader: name => {
        switch (name) {
          case 'Approved': {
            return 'approved';
          }
          case 'How old is your cat?': {
            return 'age';
          }
          case 'What is your cat\'s name?': {
            return 'name';
          }
          case 'What is your cat\'s gender?': {
            return 'gender';
          }
        }
      },
      complete: res => {
        this.categories = res.data.filter(f => {
          return f.approved === 'TRUE';
        });
        this.loadingSchedule = false;
      }
    })
  }
};
</script>
