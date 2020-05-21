<template>
  <v-container class="main-container white">
    <v-row>
      <v-col cols="12">
        <h1 class="mb-4 text-center">
          Shopping Cart 🛒
        </h1>
        <div v-if="completed == true" class="text-center thanks">
          <h1>Thanks for shopping with us! 🙌</h1>
          <br />
          <v-btn to="/" text class="pink" dark x-large>
            <span>Home</span>
          </v-btn>
        </div>
        <!-- cart is not empty -->
        <v-card v-if="cart.items.length > 0">
          <v-card-text>
            <v-list>
              <v-list-item v-for="item in cart.items" :key="item.id">
                <v-list-item-content>
                  <v-list-item-title>🍰 {{ item.name }}</v-list-item-title>
                </v-list-item-content>
                <v-list-item-content>
                  <v-list-item-subtitle
                    >$ {{ item.price }}</v-list-item-subtitle
                  >
                </v-list-item-content>
                <v-list-item-content>
                  <v-text-field
                    type="number"
                    :value="item.quantity"
                    @change="change($event, item.id)"
                  />
                </v-list-item-content>
                <v-list-item-action>
                  <v-list-item-subtitle
                    >$
                    {{
                      (item.quantity * item.price).toFixed(2)
                    }}</v-list-item-subtitle
                  >
                </v-list-item-action>
              </v-list-item>
            </v-list>
            <v-list>
              <v-list-item>
                <v-spacer />
                <v-list-item-action>
                  <v-list-item-action-text v-if="calculating" class="title"
                    >Calculating...</v-list-item-action-text
                  >
                  <v-list-item-action-text v-else class="title"
                    >$ {{ cart.total }}</v-list-item-action-text
                  >
                </v-list-item-action>
              </v-list-item>
            </v-list>
            <v-row>
              <v-spacer />
              <v-btn color="green darken-4" text to="/"
                >Continue Shopping</v-btn
              >
              <v-btn color="purple darken-4" @click="createOrder" dark
                >Checkout</v-btn
              >
            </v-row>
          </v-card-text>
        </v-card>
        <!-- cart is empty -->
        <div v-else-if="completed == false" class="text-center empty-cart">
          <h3>Your cart is empty</h3>
          <br />
          <v-btn to="/shop" text class="pink" dark x-large>
            <span>Browse Shop</span>
          </v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapGetters } from "vuex";
import { db } from "../plugins/firebase";
export default {
  name: "Cart",
  data() {
    return {
      cart: { items: [] },
      calculating: false,
      completed: false,
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
      await this.$bind("cart", db.collection("cart").doc(this.user.uid));
    },
    async change(newQty, itemId) {
      this.calculating = true;
      const theCart = this.cart;
      this.cart.items.map((item) =>
        item.id == itemId ? (item.quantity = newQty) : null
      );
      await db
        .collection("cart")
        .doc(this.user.uid)
        .set(theCart);
      this.calculating = false;
    },
    async createOrder() {
      await db.collection("orders").add({
        user: this.user.uid,
        order: this.cart,
      });
      await db
        .collection("cart")
        .doc(this.user.uid)
        .set({
          items: [],
          total: 0,
        });
      this.completed = true;
    },
  },
};
</script>

<style>
.empty-cart {
  padding: 2em;
}
.thanks {
  padding: 2em;
}
</style>
