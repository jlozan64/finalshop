<template>
<div id="bgcolor">
  <v-container>
    <v-row>
        <h2
          class="text-4xl font-light px-4 hover:bg-white hover:text-pink-800"
        >
         Crafted with love!
        </h2>
    </v-row>
    <v-row>
      <v-col
        v-for="product in products"
        :key="product.id"
        cols="12"
        md="6"
        lg="4"
      >
        <v-card>
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
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import { db } from "../plugins/firebase";
export default {
  name: "Home",
  data() {
    return {
      products: []
    };
  },
  computed: {
    ...mapGetters({
      user: "getUser"
    })
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
            price: product.price
          })
        });
    }
  }
};
</script>

<style lang="scss" scoped>
#bgcolor {
  background-color: #7fffd4;
  height: 100vh;
  background-position: center;
  background-repeat: no-repeat;
  background: relative;
}
</style>