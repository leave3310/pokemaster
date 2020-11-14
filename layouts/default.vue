<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="orange--text">頁面切換</v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn @click="light" class="mr-2">
        <v-icon>mdi-brightness-6</v-icon>
        {{ this.$vuetify.theme.dark ? '開' : '關' }}燈</v-btn
      >
      <v-btn :to="{ name: routername.name }" nuxt class="orange--text">
        <v-icon color="red">mdi-heart</v-icon>
        {{ `回${routername.route}頁面` }}
      </v-btn>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  computed: {
    routername() {
      return this.$route.name === 'index'
        ? { name: 'plz', route: '按鈕' }
        : { name: 'index', route: '首頁' }
    },
  },
  methods: {
    light() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark
    },
  },
  created() {
    // eslint-disable-next-line no-console
    console.log(this.$router.options.routes)
  },
}
</script>
