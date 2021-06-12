<template>
  <v-app dark>
    <v-app-bar app color="green" dense dark>
      <v-app-bar-nav-icon style="display: none"></v-app-bar-nav-icon>
      <v-btn @click="$router.back()" icon>
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      <v-toolbar-title class="pa-0">Form</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn @click="logoutHandler" icon>
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {
    logoutHandler() {
      localStorage.clear()
      this.$router.push('/auth/login')
    },
  },
}
</script>
