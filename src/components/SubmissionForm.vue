<template>
  <div>
    {{ active }}
  </div>
</template>

<script lang="ts">
import Vue, { PropOptions } from "vue";
import Submission from "../App.vue";

export default Vue.extend({
  name: "SubmssionForm",
  props: {
    active: {
      type: Object,
      required: true
    } as PropOptions<Submission>
  }
});
</script>

<style scoped></style>
