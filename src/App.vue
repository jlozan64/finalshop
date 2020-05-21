<template>
  <v-app>
    <NavBar />
    <v-content class="content">
      <router-view />
    </v-content>
    <Footer />
  </v-app>
</template>

<script>
import NavBar from "@/components/NavBar.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "App",
  components: {
    NavBar,
    Footer,
  },
};
</script>

<style>
.content {
  background-image: url("/images/background.jpg");
  background-repeat: repeat;
}
.main-container {
  border-radius: 20px;
  margin-top: 2em;
  margin-bottom: 2em;
  box-shadow: 1px 1px 17px grey;
}
</style>
