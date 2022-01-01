<template>
  <div>
    <h3>Account Information</h3>
    <form @submit.prevent="InfoSubmit">
      <dic class="mb-3">
        <v-text-field label="First Name" v-model="user.first_name"/>
      </dic>
      <dic class="mb-3">
        <v-text-field label="Last Name" v-model="user.last_name"/>
      </dic>
      <dic class="mb-3">
        <v-text-field label="Email" type="email" v-model="user.email"/>
      </dic>
      <v-button color="primary" type="submit">Save</v-button>
    </form>

    <h3 class="mt-4">Change Password</h3>
    <form @submit.prevent="PasswordSubmit">
      <dic class="mb-3">
        <v-text-field label="Password" v-model="first_name"/>
      </dic>
      <dic class="mb-3">
        <v-text-field label="Password Confirm" v-model="last_name"/>
      </dic>
      <v-button color="primary" type="submit">Save</v-button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Profile",
  data() {
    return {
      password: '',
      password_confirm: ''
    }
  },
  methods: {
    async infoSubmit() {
      const {data} = await axios.put('users/info', {
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        email: this.user.email
      });

      await this.$store.dispatch('setUser', data);
    },
    async PasswordSubmit() {
      await axios.put('users/password', {
        password: this.password,
        password_confirm: this.password_confirm
      })
    }
  },
  computed: {
    user() {
      return this.$store.state.user;
    }
  }
}
</script>
