<template>
  <v-card>
    <v-card-title>Form A</v-card-title>
    <v-card-text class="px-8">
      <v-row justify="space-between">
        <div>Name</div>
        <div>{{ bio.firstName }} {{ bio.lastName }}</div>
      </v-row>
      <v-row justify="space-between">
        <div>Identification Number</div>
        <div>{{ bio.idNum }}</div>
      </v-row>
      <v-row justify="space-between">
        <div>Birthplace</div>
        <div>{{ bio.birthplace }}</div>
      </v-row>
      <v-row justify="space-between">
        <div>Birth Date</div>
        <div>{{ bio.birthdate }}</div>
      </v-row>
      <v-row justify="space-between">
        <div>Phone Number</div>
        <div>{{ bio.phone }}</div>
      </v-row>
      <v-row class="mt-7 d-block">
        <v-text-field
          color="green"
          label="Question A"
          outlined
          v-model="form.QuestionA"
          dense
        ></v-text-field>
        <v-text-field
          color="green"
          label="Question B"
          outlined
          v-model="form.QuestionB"
          dense
        ></v-text-field>
        <v-text-field
          color="green"
          label="Question C"
          outlined
          v-model="form.QuestionC"
          dense
        ></v-text-field>
      </v-row>
      <v-btn @click="saveForm" color="green" class="text-capitalize" dark block
        >Save Form</v-btn
      >
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  created() {
    this.bio = JSON.parse(localStorage.getItem('data'))
    this.form.userId = this.bio._id
    this.$axios
      .get(
        `https://form-sig-server.herokuapp.com/question-a/${this.form.userId}`
      )
      .then((res) => {
        if (!res.data) return
        this.form = res.data
      })
      .catch((err) => {
        return
      })
  },
  data() {
    return {
      bio: {},
      form: {
        userId: '',
        QuestionA: '',
        QuestionB: '',
        QuestionC: '',
      },
    }
  },
  methods: {
    saveForm() {
      this.$axios
        .post('https://form-sig-server.herokuapp.com/question-a', this.form)
        .then((res) => {
          console.log('Success')
        })
    },
  },
}
</script>

<style>
</style>