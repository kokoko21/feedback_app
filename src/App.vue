<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <router-link to="/">
        <div class="text-h4 font-weight-light white--text">
          Feedback / Bug
        </div>
      </router-link>

      <v-spacer></v-spacer>

      <v-btn v-if="!login" to="/login" text small class="pr-0">
        <span class="mr-2"><v-icon>mdi-login</v-icon></span>
      </v-btn>
      <v-btn v-else to="/logout" text small class="pr-0">
        <span class="mr-2"><v-icon>mdi-logout</v-icon></span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data: () => ({
    login: false,
  }),
};
</script>
