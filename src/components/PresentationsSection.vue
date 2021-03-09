<template>
  <section class="pb-8" id="presentations">
    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row justify="center">
            <v-col cols="12" md="7">
              <template>
                <v-expansion-panels>
                  <v-expansion-panel v-for="(category,i) in categories" :key="i">
                    <v-expansion-panel-header>
                      {{ category[0] }}
                    </v-expansion-panel-header>
                    <v-expansion-panel-content>
                      <v-simple-table>
                        <thead>
                        <tr>
                          <th>Nom de la categorie / Category Name</th>
                          <th>Description du projet / Project Description</th>
                          <th>Lien Zoom / Zoom Link</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr>
                          <td>{{ category[0] }}</td>
                          <td><a :href="category[1]">{{ category[1] }}</a></td>
                          <td><a :href="category[2]">{{ category[2] }}</a></td>
                        </tr>
                        </tbody>
                      </v-simple-table>
                      <br>
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
                        <tr v-for="project in projects[i]">
                          <td>{{ project[0] }}</td>
                          <td>{{ project[1] }}</td>
                          <td>{{ project[2] }}</td>
                          <td><a :href="project[3]">{{ project[3] }}</a></td>
                        </tr>
                        </tbody>
                      </v-simple-table>
                    </v-expansion-panel-content>
                  </v-expansion-panel>
                  <div v-if="loadingSchedule">Loading schedule - please stand by...</div>
                </v-expansion-panels>
              </template>

              <br>
              <v-divider/>
              <br>

              <p class="text-justify">
                Rejoignez-nous dans l'appel zoom principal pour la cérémonie de remise des prix et les remarques de
                clôture à 14h avec ce lien : <a :href="zoom_link">{{ zoom_link }}</a>
              </p>
              <p class="text-justify">
                Vous pouvez trouver une liste des gagnants <a
                  href="https://genie.uottawa.ca/cgec/concours-etudiant/journee-du-design"
                  alt="Site pour la journée du design">ici</a>.
              </p>

              <p class="text-justify">
                Please join us back in the main zoom call for the award ceremony and closing remarks at 14h with this
                link :
                <a :href="zoom_link">{{ zoom_link }}</a>
              </p>

              <p class="text-justify">
                You can find the list of winners <a
                  href="https://engineering.uottawa.ca/ceed/student-competitions/design-day" alt="Design Day Website">here</a>.
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
    i: 0,
    size: 0,
    categories: [],
    projects: [],
    loadingSchedule: true,
    sheetURL: "https://docs.google.com/spreadsheets/d/e/2PACX-1vR9YSSnja_bENwPrcqw3lpEI_oZ3BeydmZyLwvfeUEpJB_rkqTm_U2reZHUgVdptFkmssCfzxrNxUX1/pub?output=csv"
  }),
  props: ['zoom_link'],
  created() {
    this.$papa.parse(this.sheetURL, {
      download: true,
      step: (results, parser) => {
        if (this.i === 1) {
          this.size = (results.data.length + 1) / 5;
          this.projects = new Array(this.size);
          this.categories = new Array(this.size);
          for (let i = 0; i < this.size; i++) {
            this.projects[i] = new Array();
            this.categories[i] = results.data.slice(i*5, (i*5) + 3)
          }
        } else if (this.i >= 4) {
          let cat = 0;
          let array = [];
          for (let i = 0; i < results.data.length; i++) {
            if (((i + 1) % 5) === 0) {
              this.projects[cat].push(array);
              array = [];
              cat += 1;
            } else {
              array.push(results.data[i]);
            }
          }
          this.projects[cat].push(array);
        }
        this.i++;
      },
      complete: res => {
        this.loadingSchedule = false;
      }
    })
  }
};
</script>
