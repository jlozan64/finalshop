<template>
  <v-card class="mx-auto main" max-width="300">
    <v-img src="/images/logo.png" height="100px"></v-img>

    <v-card-title>
      <h1 class="subtitle">Tina's Pastries</h1>
    </v-card-title>

    <v-card-subtitle>
      Login
    </v-card-subtitle>
    <v-card-content>
      <div id="firebaseui-auth-container" class="mt-8"></div>
      <br />
    </v-card-content>
  </v-card>
</template>

<script>
export default {
  name: "Login",
  mounted() {
    const uiConfig = {
      callbacks: {
        signInSuccessWithAuthResult: async (data) => {
          this.$store.dispatch("setUser", data.user);
          this.$router.push("/");
          return false;
        },
      },
      signInOptions: [
        this.$firebase.auth.GoogleAuthProvider.PROVIDER_ID,
        this.$firebase.auth.EmailAuthProvider.PROVIDER_ID,
      ],
    };
    this.$firebaseui.start("#firebaseui-auth-container", uiConfig);
  },
};
</script>

<style>
.subtitle {
  font-family: "Dancing Script", cursive;
}
.main {
  margin: 2em 0 2em 0;
}
</style>
