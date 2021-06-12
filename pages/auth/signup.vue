<template>
  <v-row align="center" justify="center" style="height: 100vh">
    <v-card width="100%" max-width="500px" class="pa-5 mx-5">
      <v-text-field
        v-model="form.firstName"
        color="green"
        label="First Name"
        outlined
      ></v-text-field>
      <v-text-field
        v-model="form.lastName"
        color="green"
        label="Last Name"
        outlined
      ></v-text-field>
      <v-text-field
        v-model="form.idNum"
        color="green"
        label="Identification Number"
        outlined
      ></v-text-field>
      <v-text-field
        v-model="form.birthplace"
        color="green"
        label="Birthplace"
        outlined
      ></v-text-field>
      <v-dialog
        ref="dialog"
        v-model="modal"
        :return-value.sync="form.birthdate"
        persistent
        width="290px"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            color="green"
            outlined
            v-model="form.birthdate"
            label="Birthdate"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="form.birthdate"
          color="green"
          scrollable
          light
          @update:picker-date="pickerUpdate($event)"
        >
          <v-spacer></v-spacer>
          <v-btn text color="blue lighten-2" @click="modal = false"
            >Cancel</v-btn
          >
          <v-btn
            text
            color="blue lighten-2"
            @click="$refs.dialog.save(form.birthdate)"
            >OK</v-btn
          >
        </v-date-picker>
      </v-dialog>
      <v-text-field
        v-model="form.phone"
        color="green"
        label="Phone Number"
        outlined
      ></v-text-field>
      <v-text-field
        v-model="form.email"
        color="green"
        label="Email"
        outlined
      ></v-text-field>
      <v-text-field
        v-model="form.password"
        color="green"
        label="Password"
        type="password"
        outlined
      ></v-text-field>
      <v-btn @click="sendForm" color="green" block dark class="text-capitalize"
        >Sign Up</v-btn
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
        firstName: '',
        lastName: '',
        idNum: '',
        birthplace: '',
        birthdate: '',
        phone: '',
        email: '',
        password: '',
      },
      modal: false,
    }
  },
  methods: {
    pickerUpdate: function (val) {
      // console.log(val)
      console.log(val)
    },
    sendForm() {
      this.$axios
        .post('https://form-sig-server.herokuapp.com/users', this.form)
        .then((res) => {
          this.$router.push('/auth/login')
        })
    },
  },
}
</script>

<style>
</style>