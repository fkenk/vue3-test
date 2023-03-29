<template>
  <div class="home">
    <FormTemplate />
    <GridContainer />
  </div>
</template>

<script>
import FormTemplate from '@/components/FormTemplate.vue'
import GridContainer from '@/components/GridContainer.vue'

export default {
  name: 'HomeView',
  components: {
    FormTemplate,
    GridContainer
  }
}
</script>
