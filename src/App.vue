<template>
  <v-app>
    <v-main>
      <helloworld />
    </v-main>
  </v-app>
</template>
<script>
import { defineComponent } from 'vue'
import helloworld from './components/helloworld.vue'

export default defineComponent({
  name: 'App',

  components: {
    helloworld,
  },

  setup() {
    // Data goes here
    return {}
  }
})
</script>
