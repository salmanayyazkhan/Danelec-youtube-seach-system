<template>
  <v-app>
    <v-navigation-drawer v-model="showMenu" app>
      <v-list dense v-if="showMenu">
        <v-list-item @click="navigateTo('/HOME')">
          <v-list-item-action>
            <v-icon class="home-icon">mdi-home</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item @click="navigateTo('/YouTubeSearch')">
          <v-list-item-action>
            <v-icon class="youtube-icon">mdi-youtube</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>YouTube Search</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="blue" dark>
      <v-app-bar-nav-icon @click.stop="showMenu = !showMenu"></v-app-bar-nav-icon>
      <v-toolbar-title>Danelec Candidate Assignment</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<style>

.home-icon {
  /* Add your custom styles here */
  color: dodgerblue !important;
  font-size: 24px !important;
  /* ... */
}


.youtube-icon {
  /* Add your custom styles here */
  color: red !important;
  font-size: 24px !important;
  /* ... */
}

</style>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloCandidate from "@/components/HelloCandidate.vue";

@Component({
  name: "App",
  components: { HelloCandidate },
})
export default class App extends Vue {
  showMenu: boolean = false;

  navigateTo(path: string) {
    if (this.$route.path !== path) {
      this.$router.push(path);
    }
    this.showMenu = false;
  }
}
</script>
