<template>
  <v-row class="pa-3">
    <v-card
      v-for="(form, index) in forms"
      :key="index"
      class="pa-5 ma-1"
      width="100%"
    >
      <v-row align="center" justify="space-between">
        <div>{{ form.name }}</div>
        <v-btn color="green" small dark :to="form.to">Fill In</v-btn>
      </v-row>
    </v-card>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      forms: [
        { name: 'Form A', to: '/form/A' },
        { name: 'Form B', to: '/form/B' },
      ],
    }
  },
}
</script>

<style>
</style>