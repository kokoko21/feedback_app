<template>
  <v-row>
    <v-col cols="6">
      <feedback></feedback>
    </v-col>
    <v-col cols="6">
      <bug></bug>
    </v-col>
  </v-row>
</template>

<script>
import Feedback from '../components/Feedback'
import Bug from '../components/Bug.vue'

export default {
  name: 'Home',
  components: {
    Feedback,
    Bug
  },
  data: () => ({
    login: false,
  }),
};
</script>