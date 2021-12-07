<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center"></div>
      <v-app-bar-nav-icon @click="toggleSideMenu"></v-app-bar-nav-icon>
      <span>My address book</span>
      <v-spacer></v-spacer>
    </v-app-bar>
    <SideNav></SideNav>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { mapActions } from "vuex";
import SideNav from "@/components/SideNav.vue";
import Vue from "vue";

export default Vue.extend({
  name: "App",
  components: {
    SideNav,
  },
  data: () => ({
    //
  }),
  methods: {
    ...mapActions(["toggleSideMenu"]),
  },
});
</script>
