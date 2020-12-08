<template>
  <v-container class="py-8 px-6" fluid>
    <v-col>{{ feed }}</v-col>
    <v-row>
      <!-- <v-col v-for="(feed, url, i) in feeds" :key="url" cols="12">
	<slide-y-reverse-transition>
        <v-card rounded hover>
          <v-subheader>{{ url }}</v-subheader>
          
          <v-list two-line>
            <template v-for="index in 5">
              <v-list-item :key="url-index">
                <v-list-item-avatar color="grey darken-1"> </v-list-item-avatar>

                <v-list-item-content>
                  <v-list-item-title>{{ feed[index].title }}</v-list-item-title>

                  <v-list-item-subtitle>{{ feed[index].link }}</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>

              <v-divider v-if="index !== 5" :key="`divider-${index}`" inset></v-divider>
            </template>
          </v-list>
        </v-card>
	</slide-y-reverse-transition>
      </v-col> -->
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import { mapState } from 'vuex';

export default {
  name: "Feed",
  props: ["url"],
  data: () => ({
    feed: {},
  }),
  methods: {
    getFeed(url) {
      let foundSource = this.sources.find(el => el.includes(url));
      this.feed = this.feeds[url] || {};
    }
  },
  computed: mapState({
    sources: state => state.sources,
    feeds: state => state.feeds,
  }),
  watch:{
    $route (to, from){
      this.getFeed(this.url);
    }
  },
  mounted() {
    this.getFeed(this.url);
  }
};
</script>
