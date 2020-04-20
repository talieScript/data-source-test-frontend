<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-btn @click="menu = !menu" text>
          <v-icon>mdi-menu</v-icon>
          <span class="ml-2">Submissions</span>
        </v-btn>
      </div>

      <v-spacer></v-spacer>

      <v-img
        alt="Stratum Logo"
        class="shrink mr-2"
        contain
        src="https://res-2.cloudinary.com/crunchbase-production/image/upload/c_lpad,h_256,w_256,f_auto,q_auto:eco/41873246e73b8cf3ed5f"
        transition="scale-transition"
        width="150"
      />
    </v-app-bar>

    <v-navigation-drawer v-model="menu" absolute temporary>
      <SubmissionsList :submissions="submissions" />
    </v-navigation-drawer>

    <v-content>
      <HelloWorld />
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import SubmissionsList from "./components/SubmissionsList.vue";
import fakeSubmssions from "./dummyData/submissions.ts";

export interface Submission {
  id: number;
  vesselName: string;
  vesselImo: number;
  dateTime: {
    // iso string
    date: string;
    // unix timestamp
    timeStamp: number;
    // + or - offset
    offSet: number;
  };
  fuels: {
    LGO: number;
    IFO: number;
    MGO: number;
  };
  // sum of fuels
  totalFuel: number;
}

export default Vue.extend({
  name: "App",
  components: {
    HelloWorld,
    SubmissionsList
  },
  data() {
    return {
      menu: true,
      submissions: []
    };
  },
  mounted() {
    this.submissions = fakeSubmssions;
  }
});
</script>
