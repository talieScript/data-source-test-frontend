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
      <SubmissionsList
        @changeSubmission="changeActiveSubmission"
        :submissions="submissions"
      />
    </v-navigation-drawer>

    <v-content>
      <submssion-form
        v-if="activeSubmission.id"
        @submit="submit"
        :active="activeSubmission"
      />
    </v-content>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import SubmissionsList from "./components/SubmissionsList.vue";
import fakeSubmssions from "./dummyData/submissions";
import SubmssionForm from "./components/SubmissionForm.vue";

export interface Submission {
  id: number;
  vesselName: string;
  vesselImo: number;
  dateOffset: {
    // iso string
    date: string;
    // + or - offset
    offset: number;
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
    SubmissionsList,
    SubmssionForm
  },
  data() {
    return {
      menu: true,
      submissions: [],
      activeSubmission: {}
    };
  },
  methods: {
    setActiveSubmission(value) {
      this.activeSubmission = value;
    },
    changeActiveSubmission(id: string) {
      this.activeSubmission = this.submissions.find(submission => {
        return submission.id == id;
      }) as Submission;
    },
    /**
     * submit function here
     */
    submit(submission) {
      console.log(submission);
    }
  },
  mounted() {
    this.submissions = fakeSubmssions;
    this.activeSubmission = this.submissions[0];
  }
});
</script>
