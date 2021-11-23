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
                          <th class="body-2 black--text font-weight-bold">Nom de la categorie / Category Name</th>
                          <th class="body-2 black--text font-weight-bold" v-if="i <= 4">Description du projet / Project Description</th>
                          <th class="body-2 black--text font-weight-bold">Lien Zoom / Zoom Link</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr>
                          <td>{{ category[0] }}</td>
                          <td v-if="i <= 4"><a target="_blank" :href="category[1]">{{ category[1] }}</a></td>
                          <td><a target="_blank" :href="category[2]">{{ category[2] }}</a></td>
                        </tr>
                        </tbody>
                      </v-simple-table>
                      <br>
                      <v-simple-table>
                        <thead>
                        <tr>
                          <th class="body-2 black--text font-weight-bold">Breakout Room</th>
                          <th class="body-2 black--text font-weight-bold">Groupe / Groupe</th>
                          <th class="body-2 black--text font-weight-bold">Heure / Time</th>
                          <th class="body-2 black--text font-weight-bold" v-if="i <= 4">Répertoire de projet / Project repository</th>
                          <th class="body-2 black--text font-weight-bold" v-if="i > 4">Projet / Project</th>
                          <th class="body-2 black--text font-weight-bold" v-if="i === 5">Description du projet / Project description</th>
                          <th class="body-2 black--text font-weight-bold" v-if="i === 5">Lien du Projet / Project Repository</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="project in projects[i]" v-if="project[0] !== '' || project[1] !== '' || project[2] !== '' || project[3] !== ''">
                          <td>{{ project[0] }}</td>
                          <td>{{ project[1] }}</td>
                          <td>{{ project[2] }}</td>
                          <td v-if="i <= 4" ><a target="_blank" :href="project[3]">{{ project[3] }}</a></td>
                          <td v-if="i === 5">{{ project[3] }}</td>
                          <td v-if="i === 5"><a target="_blank" :href="project[4]">{{project[1].includes("FA") ? "lien" : "link" }}</a></td>
                          <td v-if="i === 5"><a target="_blank" :href="project[5]">{{ project[5] }}</a></td>
                          <td v-if="i === 6">{{ project[3] }}</td>
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
                clôture à 15h avec ce lien : <a target="_blank" :href="zoom_link">{{ zoom_link }}</a>
              </p>
              <p class="text-justify">
                Vous pouvez trouver une liste des gagnants <a
                  href="https://genie.uottawa.ca/cgec/concours-etudiant/journee-du-design"
                  alt="Site pour la journée du design">ici</a>.
              </p>

              <p class="text-justify">
                Please join us back in the main zoom call for the award ceremony and closing remarks at 15h with this
                link :
                <a target="_blank" :href="zoom_link">{{ zoom_link }}</a>
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
    i: 0, // Index for the projects
    size: 0, // Total number of categories when the 2 csvs are grouped
    second_size: 0, // Number of categories in the first csv file
    categories: [], // Categories Array
    projects: [], // Projects Array
    loadingSchedule: true, // OnLoad message for schedule
    sheetURL: [
        "https://docs.google.com/spreadsheets/d/e/2PACX-1vSi3-oy7YOjfsmKDcAluyiEHY5K7RuB77oQVvd6YALeUcA6yLcWfjCZ-AWIOf5nc1w0zYsHSG3XVRf4/pub?output=csv",
        "https://docs.google.com/spreadsheets/d/e/2PACX-1vSi3-oy7YOjfsmKDcAluyiEHY5K7RuB77oQVvd6YALeUcA6yLcWfjCZ-AWIOf5nc1w0zYsHSG3XVRf4/pub?output=csv&gid=472575453"
    ] // Array with the 2 CSVs
  }),
  props: ['zoom_link'],
  created() {
    this.$papa.parse(this.sheetURL[0], {
      download: true,
      step: (results) => {
        if (this.i === 1) { // If Categories header
          this.size = (results.data.length + 1) / 5; // Determine number of categories
          this.projects = new Array(this.size); // Creating the right size array for the first projects
          this.categories = new Array(this.size); // Creating the right size array for the first categories
          for (let i = 0; i < this.size; i++) { // Looping around the categories to create the empty arrays and inserting categories
            this.projects[i] = [];
            this.categories[i] = results.data.slice(i*5, (i*5) + 3)
          }
        } else if (this.i >= 4) { // If Projects
          let cat = 0; // Category Index
          for (let i = 0; i < results.data.length; i+=5) {
            this.projects[cat].push(results.data.slice(i, i+4));
            cat += 1;
          }
        }
        this.i++;
      },
      complete: res => {
        this.i = 0;
        this.$papa.parse(this.sheetURL[1], {
          download: true,
          step: (results) => {
            if (this.i === 1) { // If Categories header
              this.second_size = this.size; // Size of previous categories part
              this.size += Math.ceil((results.data.length + 1) / 6); // Size of all categories
              for (let i = this.second_size; i < this.size; i++) { // Adding to the categories and projects array
                this.categories.push([]);
                this.projects.push([]);
                this.projects[i] = [];
                this.categories[i] = [results.data[(i-this.second_size)*7], "", results.data[(i-this.second_size)*7+1]]
              }
            } else if (this.i >= 4) { // If projects
              let cat = this.second_size; // Category index starting from previous index
              for (let i = 0; i < results.data.length; i+=7) {
                this.projects[cat].push(results.data.slice(i, i+6));
                cat += 1;
              }
            }
            this.i++;
          },
          complete: res => {
            this.loadingSchedule = false;
          }
        })
      }
    })
  }
};
</script>
