<template>
  <v-app>
    <v-main>
      <TeamMatching />
    </v-main>
  </v-app>
</template>

<script>
import TeamMatching from './components/TeamMatching.vue'


export default {
  name: 'App',

  components: {
    TeamMatching,
  },

  data: () => ({
    //
  }),
}
</script>
