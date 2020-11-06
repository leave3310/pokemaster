<template>
  <div>
    <v-app>
      <nuxt />
    </v-app>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: '',
      pages: '',
    }
  },
  methods: {
    routername() {
      if (this.$route.name === 'index') {
        this.display = '首頁'
        return 'plz'
      } else {
        this.display = '按鈕'
        return 'index'
      }
    },
  },
}
</script>
