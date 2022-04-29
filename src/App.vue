<template>
  <v-app>

    <v-main>
      <SectionComponents/>
    </v-main>
  </v-app>
</template>

<script>
import SectionComponents from './components/SectionComponents';

export default {
  name: 'App',

  components: {
    SectionComponents,
  },

  data: () => ({
    //
  }),
};
</script>
