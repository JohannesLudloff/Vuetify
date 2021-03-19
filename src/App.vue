<template>
  <v-app class="">
    <Navbar />
    <v-main class="grey lighten-4 px-4 ">
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  name: "App",

  components: {
    Navbar,
  },

  data: () => ({
    //
  }),
};
</script>
