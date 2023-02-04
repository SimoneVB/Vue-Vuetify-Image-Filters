<template>
  <v-app>
    <v-main>
      <image-filters />
    </v-main>
  </v-app>
</template>

<script>
import ImageFilters from './components/image-filters.vue'

export default {
  name: 'App',

  components: {
    ImageFilters,
  },
}
</script>
