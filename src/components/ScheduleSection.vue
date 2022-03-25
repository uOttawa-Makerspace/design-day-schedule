<template>
  <section class="pb-8" id="schedule">
    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="10">
          <v-row align="center" justify="center">
            <v-col cols="12" md="7">
              <br><br>
              <h1 class="font-weight-light display-2">Horaire / Schedule</h1>
              <h1 class="font-weight-light display-1 mb-3">
                31/03/2022
              </h1>
              <v-row>
                <v-col>
                  <p class="text-justify">
                    Bienvenue à la journée de design de l'hiver 2022. Ce programme vous permettra de vous orienter
                    durant toutes les présentations. Rejoignez-nous dans l'appel zoom principal pour les remarques
                    d'ouverture à 9h30 avec ce lien zoom: <a
                      target="_blank" :href="zoom_link">{{ zoom_link }}</a>
                  </p>
                  <p class="text-justify">
                    Welcome to the Winter 2022 Design day. This program will allow you to orient yourself during all the
                    presentations. Please join us in the main zoom call for the opening remarks at 9:30am with this zoom
                    link: <a
                      target="_blank" :href="zoom_link">{{ zoom_link }}</a>
                  </p>
                </v-col>
              </v-row>
              <v-simple-table fixed-header>
                <template v-slot:default>
                  <thead>
                  <tr>
                    <th class="text-left body-2 black--text font-weight-bold">
                      Heure / Time
                    </th>
                    <th class="text-left body-2 black--text font-weight-bold">
                      Événement / Event
                    </th>
                  </tr>
                  </thead>
                  <tbody>
                  <tr
                      v-for="item in events">
                    <td>{{ item.time }}</td>
                    <td>{{ item.description }}</td>
                  </tr>
                  </tbody>
                </template>
              </v-simple-table>
              <v-row>
                <v-col>
                  <br>
                  <p class="text-justify">
                    Les séries de présentations suivantes auront lieu en parallèle. Le format des présentations est le
                    suivant :
                  <ul>
                    <li>Chaque groupe présentera pendant 3 minutes</li>
                    <li>Il y aura 5 minutes de question par groupe</li>
                  </ul>
                  </p>
                  <p class="text-justify">
                    The following sets of presentations will happen in parallel. The format of the presentations is the
                    following:
                  <ul>
                    <li>Each group will present for 3 minutes</li>
                    <li>There will be 5 minutes for questions per group</li>
                  </ul>
                  </p>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <div class="svg-border-waves text-white">
      <v-img src="~@/assets/img/borderWaves.svg"/>
    </div>
  </section>
</template>
<script>
export default {
  data: () => ({
    events: [
      {
        time: '9h-9h30',
        description: 'Orientation des juges / Judge orientation',
      },
      {
        time: '9h30-9h45',
        description: 'Remarques d’ouverture / Opening remarks',
      },
      {
        time: '10h-12h',
        description: 'Présentations / Presentations',
      },
      {
        time: '12h30-12h50',
        description: 'Remarques de clôture et cérémonie de remise des prix / Closing remark and awards ceremony',
      },
    ],
  }),
  props: ['zoom_link'],
}
</script>
<style scoped>
#schedule {
  background-color: #f4f7f5;
}

.svg-border-waves .v-image {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 3rem;
  width: 100%;
  overflow: hidden;
}
</style>
