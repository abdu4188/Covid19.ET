<template>
  <v-content class="d-flex justify-md-space-around vertical-center ">
    <v-card
      max-width="480"
      width="380"
      :loading="loading"
      lg="6"
      md="8"
      sm="10"
      xs="11"
      class=" my-auto px-8 py-3"
    >
      <v-card-title>Covid19.ET</v-card-title>
      <v-card-subtitle>Log in</v-card-subtitle>
      <v-card-text>
        <v-alert color="warn" dark dense dismissible v-if="error">{{
          error
        }}</v-alert>
        <v-row class="mt-6">
          <v-text-field
            outlined
            rounded
            dense
            v-model="username"
            label="Phone/email"
          ></v-text-field>
        </v-row>

        <v-row>
          <v-text-field
            dense
            outlined
            rounded
            v-model="password"
            label="password"
          ></v-text-field>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-spacer /><v-btn @click.stop="login">Login</v-btn>
      </v-card-actions>
    </v-card>
  </v-content>
</template>

<script>
import { mapActions } from "vuex";
export default {
  layout: "login-layout",
  data() {
    return {
      username: "",
      password: "",
      loading: false,
      error: false
    };
  },
  methods: {
    ...mapActions("auth", ["authenticate"]),
    login() {
      this.error = null;
      this.loading = true;
      this.authenticate({
        user: this.username,
        password: this.password,
        strategy: "local"
      })
        .then(res => {
          this.loading = false;
          this.$router.push("/");
        })
        .catch(err => {
          this.loading = false;
          this.error = err;
        });
    }
  }
};
</script>

<style>
.vertical-center {
  margin: auto;
  position: relative;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}
</style>
