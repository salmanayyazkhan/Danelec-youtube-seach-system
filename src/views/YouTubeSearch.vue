<template>
  <div>
    <v-card class="elevation-12">
      <v-toolbar color="red" dark flat>
        <v-toolbar-title>YouTube Search</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        <v-text-field
          v-model="q"
          hide-details
          prepend-icon="mdi-magnify"
          single-line
          label="Find your favorite YouTube videos here"
          outlined
        ></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="search">Search</v-btn>
      </v-card-actions>
    </v-card>

    <v-alert type="info" v-if="v.length > 0">
      Found {{ v.length }} videos
    </v-alert>

    <v-list three-line>
      <template v-for="(item, index) in v">
        <YouTubeVideo :key="index" :video="item.video"></YouTubeVideo>
      </template>
    </v-list>
  </div>
</template>

<script lang="ts">
import {Component, Vue, Watch} from "vue-property-decorator";
import YouTubeVideo from "@/components/YouTubeVideo.vue";
import axios from "axios";
import config from "@/config";

@Component({
  name: "YouTubeSearch",
  components: {YouTubeVideo},
})
export default class YouTubeSearch extends Vue {
  q: string = "";
  r: any = null;
  v: any = [];

  search() {
    if (this.q == "") {
      console.log('please enter something first')
      return
    }
    axios
      .get(config.youtubeBaseUrl, {
        params: {
          q: this.q,
          key: config.youtubeApiKey,
          part: "snippet",
        },
      })
      .then((res) => {
        this.r = res.data;
      })
      .catch((error) => {
        if (error.response && error.response.status === 403) {
          console.error("The request cannot be completed because you have exceeded your");
        } else {
          console.error("API request failed:", error);
        }
      });
  }

  @Watch("r")
  update() {
    this.v = [];
    if (this.r && this.r.items) {
      this.r.items.forEach((item: any) => {
        this.v.push({video: item});
      });
    }
  }
}

</script>
