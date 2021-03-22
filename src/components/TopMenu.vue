<template>
  <!-- dropdown menu -->
  <v-menu offset-y>
    <template v-slot:activator="{ on, attrs }">
      <v-btn text color="primary" dark v-bind="attrs" v-on="on">
        <v-icon>mdi-chevron-down</v-icon>
        <span> menu</span>
      </v-btn>
    </template>
    <v-list>
      <v-list-item dense v-for="(item, index) in links" :key="index" router :to="item.route">
        <v-list-item-title>{{ item.text }}</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-menu>
  <!-- end dropdown -->
</template>

<script>
export default {
  props: {
    links: Array,
  },
};
</script>

<style lang="scss" scoped></style>
