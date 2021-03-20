<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-btn v-bind="attrs" v-on="on" icon>
        {{ title }}
        <v-icon color="primary">
          {{ icon }}
        </v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">Add Project</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field
                required
                label="Project Title*"
                v-model="title"
                prepend-icon="mdi-folder"
                hint="Give a unique name to your project"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-textarea label="Information" prepend-icon="mdi-pencil"></v-textarea>
            </v-col>
          </v-row>
        </v-container>
        <small>*indicates required field</small>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary darken-1" text @click="dialog = false">
          Close
        </v-btn>
        <v-btn color="primary darken-1" text @click="dialog = false">
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    title: "",
  }),
  props: {
    title: String,
    icon: String,
    props: Array,
  },
};
</script>
