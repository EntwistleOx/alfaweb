<template>
  <div>
    <v-app-bar app color="primary" dark>
      <v-app-bar-nav-icon @click.stop="showDrawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Cursos Alfaweb</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn text to="/login" v-if="!currentUser"> Login </v-btn>
      <v-btn text to="/registro" v-if="!currentUser"> Registro </v-btn>
      <v-btn text v-if="currentUser"> {{ currentUser }} </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  name: "Navbar",
  data: () => ({}),
  computed: {
    ...mapState(["user", "drawer"]),
    currentUser() {
      return this.user;
    },
  },
  methods: {
    ...mapActions(["show_Drawer"]),
    showDrawer() {
      this.show_Drawer(!this.drawer);
    },
  },
};
</script>
