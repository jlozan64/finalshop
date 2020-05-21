<template>
  <v-app-bar height="100" color="white" hide-on-scroll light app>
    <router-link
      to="/"
      style="text-decoration: none; color: black; text-align; display: contents"
    >
      <v-img
        class="mx-2"
        src="/images/logo.png"
        max-height="40"
        max-width="40"
        contain
      ></v-img>

      <v-toolbar-title class="navbar-title ml-2" style="font-size: 1.50rem;">
        Tina's Pastries
      </v-toolbar-title>
    </router-link>
    <v-spacer></v-spacer>

    <v-btn text to="/shop" class="pink" dark>
      <span>Shop</span>
    </v-btn>
    <v-btn v-if="!user" to="/login" text>
      <span>Login</span>
    </v-btn>
    <div v-else>
      <v-menu bottom left>
        <template v-slot:activator="{ on }">
          <v-btn text v-on="on">
            <span class="mr-2">{{ user.displayName }}</span>
            <v-icon>mdi-menu-down</v-icon>
          </v-btn>
          <v-badge color="blue" overlap>
            <template v-slot:badge>{{ cart.items.length }}</template>
            <v-btn text @click="$router.push('/cart')">
              <v-icon>mdi-cart</v-icon>
            </v-btn>
          </v-badge>
        </template>

        <v-list>
          <v-list-item>
            <v-list-item-title>
              <v-btn block text to="/about">About Us</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title>
              <v-btn block text to="/myorders">Orders</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title>
              <v-btn block text to="/cart">Cart</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item v-if="user.roles && user.roles.admin">
            <v-list-item-title>
              <v-btn block text to="/inventory">Inventory</v-btn>
            </v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title>
              <v-btn block text @click="logOut">Logout</v-btn>
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </div>
  </v-app-bar>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
import { db } from "../plugins/firebase";

export default {
  name: "NavBar",
  data() {
    return {
      cart: { items: [] },
    };
  },
  computed: {
    ...mapGetters({
      user: "getUser",
    }),
  },

  updated() {
    this.bind();
  },
  mounted() {
    this.bind();
  },
  methods: {
    async logOut() {
      await this.$firebase.auth().signOut();
      this.setUser("");
      this.$router.push("/");
    },
    async bind() {
      await this.$bind("cart", db.collection("cart").doc(this.user.uid));
    },
    ...mapActions(["setUser"]),
  },
};
</script>

<style>
.navbar-title {
  font-family: "Dancing Script", cursive;
  font-size: 40px;
}
</style>
