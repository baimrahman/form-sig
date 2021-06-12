<template>
  <v-row align="center" justify="center" style="height: 100vh">
    <v-card width="100%" max-width="500px" class="pa-5 mx-5">
      <v-text-field
        color="green"
        v-model="form.email"
        label="Email"
        outlined
      ></v-text-field>
      <v-text-field
        color="green"
        v-model="form.password"
        label="Password"
        type="password"
        outlined
      ></v-text-field>
      <v-btn
        @click="signinHandler"
        color="green"
        block
        dark
        class="text-capitalize"
        >Log In</v-btn
      >
      <v-btn to="/auth/signup" block text class="text-capitalize"
        >Sign Up Now!</v-btn
      >
    </v-card>
  </v-row>
</template>

<script>
export default {
  layout: 'auth',
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
    }
  },
  created() {
    localStorage.clear()
  },
  methods: {
    signinHandler() {
      this.$axios
        .post('http://form-sig-server.herokuapp.com/users/login', this.form)
        .then((res) => {
          localStorage.setItem('data', JSON.stringify(res.data))
          this.$router.push('/')
        })
    },
  },
}
</script>

<style>
</style>