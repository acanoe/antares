<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app>
      <v-sheet color="grey lighten-4" class="pa-4">
        <v-list-item to="/" :link="false">
        <v-list-item-content>
          <v-list-item-title class="title">
            Antares
          </v-list-item-title>
          <v-list-item-subtitle>
            Rss reader
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      </v-sheet>

      <v-divider></v-divider>

      <v-list rounded dense>
        <v-list-item v-for="source in sources" :key="source" :to="{ path: '/feed', query: { url: source }}" link exact>
          <v-list-item-content>
            <v-list-item-title>{{ source }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <template v-slot:append>
        <div class="pa-2">
          <v-btn block>Manage sources</v-btn>
        </div>
      </template>
    </v-navigation-drawer>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data: () => ({
    drawer: null,
  }),
  computed: mapState({
    sources: state => state.sources.map((url) => url.split('https://').pop()),
  }),
};
</script>
