<template>
  <v-footer dark padless>
    <v-card class="flex" flat tile>
      <v-card-title class="pink">
        <strong class="subheading"
          >Get connected with us on social networks!</strong
        >

        <v-spacer></v-spacer>

        <v-btn v-for="icon in icons" :key="icon" class="mx-4" dark icon>
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
      </v-card-title>

      <v-card-text class="py-2 white--text text-center teal">
        {{ new Date().getFullYear() }} —
        <strong
          >Tina's Pastries by
          <a class="link-to-me" href="https://github.com/jlozan64"
            >Janeth Lozano</a
          ></strong
        >
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  data: () => ({
    icons: ["mdi-facebook", "mdi-twitter", "mdi-linkedin", "mdi-instagram"],
  }),
};
</script>

<style>
a.link-to-me {
  color: white !important;
}
</style>
