<template>
  <v-list-item>
    <v-list-item-avatar size="100">
      <a :href="linkUrl" target="_blank">
        <v-img :src="imageUrl"></v-img>
      </a>
    </v-list-item-avatar>

    <v-list-item-content>
      <v-list-item-title>{{ title }}</v-list-item-title>
      <v-list-item-subtitle>{{ description }}</v-list-item-subtitle>
    </v-list-item-content>
  </v-list-item>
</template>

<script lang="ts">
import {Component, Model,Vue, Watch} from "vue-property-decorator";
import config from "@/config";

@Component({name: "YouTubeVideo"})
export default class YouTubeVideo extends Vue {
  @Model() video!: any;

  title: any = "";
  imageUrl: any = "";
  description: any = "";
  id: any = "";
  linkUrl: any = "";

  mounted() {
    console.log(this.video)
    this.updateVideo();
  }

  @Watch("video")
  onVideoChanged(newVideo: any) {
    this.video = newVideo;
    this.updateVideo();
  }

  updateVideo() {
    this.title = this.video.snippet.title;
    this.imageUrl = this.video.snippet.thumbnails.default.url;
    this.description = this.video.snippet.description;
    this.id = this.video.id.videoId;
    this.linkUrl = config.youtubeWatchBaseUrl + this.id;
  }
}
</script>
