<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
        class="pa-4 pt-7"
        height="170"
        src="mountains.jpg"
        gradient="to top right, rgba(19,84,122,.6), rgba(128,208,199,.8)"
      >
        <v-avatar size="70" class="mb-2">
          <img src="Avatar.jpg" alt="Srdjan Maravic" />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Srdjan Maravic
        </div>
        <div class="white--text text-subtitle-2">srdjan_maravic</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      color="primary"
      src="mountains.jpg"
      app
      dark
      prominent
      :height="$route.path === '/' ? '238' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="header-container">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
          <v-btn
            :to="link.favourites"
            link
            icon
            :disabled="$store.state.sorting"
          >
            <v-icon>mdi-heart</v-icon>
          </v-btn>
        </v-row>
        <v-row>
          <v-app-bar-title class="text-h4 ml-4">{{
            $store.state.appTitle
          }}</v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-tasks />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from "@/components/Shared/Snackbar.vue";
import Search from "@/components/Tools/Search.vue";
import LiveDateTime from "@/components/Tools/LiveDateTime.vue";
import FieldAddTask from "@/components/Todo/FieldAddTask.vue";

export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Todos", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
    link: {
      favourites: "/favourites",
    },
  }),

  components: {
    snackbar: Snackbar,
    search: Search,
    "live-date-time": LiveDateTime,
    "field-add-tasks": FieldAddTask,
  },
  mounted() {
    this.$store.dispatch("getTasks");
  },
};
</script>

<style lang="sass">
.header-container
  max-width: none !important
  .v-app-bar-title__content
    width: 100% !important
</style>
