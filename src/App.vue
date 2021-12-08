<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center"></div>
      <v-app-bar-nav-icon
        v-show="$store.state.login_user"
        @click.stop="toggleSideMenu"
      ></v-app-bar-nav-icon>
      <span>My address book</span>
      <v-spacer></v-spacer>
      <v-toolbar-items v-if="$store.state.login_user">
        <v-btn @click="logout">ログアウト</v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <SideNav></SideNav>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import firebase from "firebase";
import { mapActions } from "vuex";
import SideNav from "@/components/SideNav.vue";
import Vue from "vue";

export default Vue.extend({
  name: "App",
  components: {
    SideNav,
  },
  created() {
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.setLoginUser(user);
        if (this.$router.currentRoute.name === "Home") {
          this.$router.push({ name: "addresses" });
        }
      } else {
        this.deleteLoginUser();
        this.$router.push({ name: "Home" });
      }
    });
  },
  data: () => ({
    //
  }),
  methods: {
    ...mapActions([
      "toggleSideMenu",
      "setLoginUser",
      "logout",
      "deleteLoginUser",
    ]),
  },
});
</script>
