<template>
  <nav>
    <v-app-bar flat app>
      <v-icon left class="grey--text" @click="drawer = !drawer">mdi-menu</v-icon>
      <v-toolbar-title class="grey--text">
        <span class="font-weight-light">Todo</span>
        <span class="primary--text text--accent-2 font-weight-bold">Ninja</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <!-- dropdown menu -->
      <v-menu offset-y>
        <template v-slot:activator="{ on, attrs }">
          <v-btn text color="primary" dark v-bind="attrs" v-on="on">
            <v-icon>mdi-chevron-down</v-icon>
            <span> menu</span>
          </v-btn>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in links" :key="index" router :to="item.route">
            <v-list-item-title>{{ item.text }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <!-- end dropdown -->
      <v-btn icon color="grey">
        <v-icon>mdi-exit-to-app</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer disable-resize-watcher temporary app class="primary" v-model="drawer">
      <v-layout column align-center>
        <v-avatar size="60" class="mt-5">
          <img src="../assets/JL_Logo.png" alt="" />
        </v-avatar>
        <p class="white--text subheading mt-1">Johannes Ludloff</p>
        <Popup btn_description="Add Project" />
      </v-layout>
      <v-list>
        <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
          <v-list-item-action>
            <v-icon class="white--text">{{ link.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content class="white--text">
            {{ link.text }}
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
import Popup from "../components/Popup";
export default {
  components: { Popup },
  data() {
    return {
      drawer: false,
      links: [
        { icon: "mdi-view-dashboard", text: "Dashboard", route: "/" },
        { icon: "mdi-folder", text: "My Projects", route: "/projects" },
        { icon: "mdi-account-supervisor-circle", text: "Team", route: "/team" },
      ],
    };
  },
};
</script>
