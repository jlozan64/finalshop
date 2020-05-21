<template>
  <v-container class="white lighten-5 main-container">
    <v-row>
      <v-col class="text-center" cols="12" lg="6">
        <h1>What we do</h1>
        <v-card class="pa-2" elevation="0">
          <iframe
            width="560"
            height="315"
            src="https://www.youtube.com/embed/vASapvgu9gQ"
            frameborder="0"
            allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </v-card>
        <br />
        <v-btn to="/shop" text class="pink" dark x-large>
          <span>Browse Pastries</span>
        </v-btn>
      </v-col>
      <v-col cols="12" sm="6">
        <v-card class="pa-2" elevation="0">
          <v-card class="mx-auto">
            <v-img
              height="250"
              src="https://static1.squarespace.com/static/518ea9e4e4b0eb1ecff22776/518ea9e5e4b0eb1ecff2277a/5810deba6b8f5b70e61d54fd/1536097055223/shutterstock_176646242.jpg?format=1500w"
            ></v-img>

            <v-card-title>Tina's Pastries</v-card-title>

            <v-card-text>
              <v-row align="center" class="mx-0">
                <v-rating
                  :value="4.5"
                  color="amber"
                  dense
                  half-increments
                  readonly
                  size="14"
                ></v-rating>

                <div class="grey--text ml-4">4.5 (413)</div>
              </v-row>

              <div class="my-4 subtitle-1">
                $ • Cakeshop, Cafe
              </div>

              <div>
                Pastries decoration, party events, online store, cafe place,
                come and visit us.
              </div>
            </v-card-text>

            <v-divider class="mx-4"></v-divider>

            <v-card-title>Today's Open Hours</v-card-title>

            <v-card-text>
              <v-chip-group
                active-class="deep-purple accent-4 white--text"
                column
              >
                <v-chip>8:30AM - 12:00PM</v-chip>

                <v-chip>1:00PM- 6:00PM</v-chip>
              </v-chip-group>
            </v-card-text>
          </v-card>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {};
  },
  computed: {},
  mounted() {},
  methods: {},
};
</script>

<style lang="scss"></style>
