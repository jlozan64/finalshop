<template>
  <v-container class="main-container white">
    <v-alert
      v-if="alert != null"
      border="top"
      color="red lighten-2"
      dark
      dismissible
    >
      {{ alert }}
    </v-alert>
    <div class="text-center">
      <h1>Our selection of pastries</h1>
      <h2>
        Crafted with
        <v-icon color="red">mdi-heart</v-icon>
      </h2>
    </div>
    <v-row>
      <v-col
        v-for="product in products"
        :key="product.id"
        cols="12"
        md="6"
        lg="4"
      >
        <v-card>
          <v-img
            src="https://cdn3.tmbi.com/toh/GoogleImagesPostCard/Raspberry---Cream-Cheese-Pastries_exps152919_THCA143053B010_31_5b_RMS.jpg"
            class="white--text align-end"
            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            height="200px"
          ></v-img>
          <v-card-title class="headline">{{ product.name }}</v-card-title>
          <v-card-subtitle>
            <v-container>
              <v-row>
                <p class="title">${{ product.price }}</p>
                <v-spacer />
                <div>
                  <p v-if="product.quantity > 0" class="success--text">
                    {{ product.quantity }} left
                  </p>
                  <p v-else class="error--text">Out of Stock</p>
                </div>
              </v-row>
            </v-container>
          </v-card-subtitle>
          <v-card-text class="mt-n6">{{ product.description }}</v-card-text>
          <v-card-actions>
            <v-btn
              v-if="user"
              block
              color="pink"
              rounded
              dark
              :disabled="product.quantity == 0"
              @click="addToCart(product)"
              >Add to Cart</v-btn
            >
            <v-btn
              v-else
              block
              color="green"
              rounded
              :disabled="product.quantity == 0"
              to="/login"
              >Please Login to Buy</v-btn
            >
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapGetters } from "vuex";
import { db } from "../plugins/firebase";
export default {
  name: "Shop",
  data() {
    return {
      products: [],
      alert: null,
    };
  },
  computed: {
    ...mapGetters({
      user: "getUser",
    }),
  },
  mounted() {
    this.bind();
  },
  methods: {
    async bind() {
      await this.$bind(
        "products",
        db.collection("products").where("showCatalog", "==", true)
      );
    },
    async addToCart(product) {
      await db
        .collection("cart")
        .doc(this.user.uid)
        .update({
          items: this.$firebase.firestore.FieldValue.arrayUnion({
            id: product.id,
            name: product.name,
            quantity: 1,
            price: product.price,
          }),
        });
      this.alert = product.name + " added to cart!";

      alert(this.alert);
    },
  },
};
</script>

<style lang="scss" scoped></style>
