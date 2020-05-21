<template>
  <v-container class="main-container white text-center">
    <h1>What we do</h1>
    <v-row>
      <v-col sm="6">
        <v-img
          class="rounded"
          src="https://cdnimg.webstaurantstore.com/uploads/blog/2018/8/start-a-bakery-bakery-display-case.jpg"
          lazy-src="https://picsum.photos/id/11/100/60"
        >
          <template v-slot:placeholder>
            <v-row class="fill-height ma-0" align="center" justify="center">
              <v-progress-circular
                indeterminate
                color="grey lighten-5"
              ></v-progress-circular>
            </v-row>
          </template>
        </v-img>
      </v-col>
      <v-col sm="6" class="description">
        <h4>
          Located in Rio Grande Valley, Tina's Pastery Shop crafts all of our
          baked treats from scratch with fresh and natural ingredients. For the
          most discerning sweet tooth, we offer ready to go Cakes, Cupcakes,
          Cake Pops, French Macarons, Cookies, Pies, and much more! You can make
          a purchase through our website or visit our local shop!
        </h4>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import bgImage from "../assets/bg.jpg";
export default {
  name: "about",
  data() {
    return {
      bgImage,
    };
  },
};
</script>
<style>
.description {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
