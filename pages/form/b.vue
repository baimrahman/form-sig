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
          label="Question D"
          outlined
          v-model="form.QuestionD"
          dense
        ></v-text-field>
        <v-text-field
          color="green"
          label="Question E"
          outlined
          v-model="form.QuestionE"
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
        `http://form-sig-server.herokuapp.com/question-b/${this.form.userId}`
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
        QuestionD: '',
        QuestionE: '',
      },
    }
  },
  methods: {
    saveForm() {
      this.$axios
        .post('http://form-sig-server.herokuapp.com/question-b', this.form)
        .then((res) => {
          console.log('Success')
        })
    },
  },
}
</script>

<style>
</style>