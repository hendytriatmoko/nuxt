<template>
  <div>
    <app-bar />
    <br>

    <div>ini halaman depan</div>
  </div>
</template>

<script>

import { mapGetters, mapActions } from 'vuex'


export default {
  name: 'Home',
  components: {
    AppBar: () =>
      import(/* webpackChunkName: "app-bar" */ '@/components/AppBar.vue'),
       Footer: () =>
      import(/* webpackChunkName: "footer" */ '@/components/Footer.vue'),
  },
  data: () => ({
    
  }),
  computed: {
    ...mapGetters({
      utc: 'timezone/utc',
      timezone: 'timezone/region',
    }),
  },
  methods: {
    ...mapActions({
      setSellertId: 'product/setSeller',
      setProductId: 'product/setProduct',
    }),

  },
  async created() {
    
  },
}
</script>

<style scoped>
</style>
