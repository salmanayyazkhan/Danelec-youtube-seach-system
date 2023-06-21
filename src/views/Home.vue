<template>
  <v-main>
    <HelloCandidate />
  </v-main>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloCandidate from "@/components/HelloCandidate.vue";

@Component({
  name: "Home",
  components: { HelloCandidate },
})
export default class Home extends Vue {}
</script>
