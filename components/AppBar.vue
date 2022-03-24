<template>
  <div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'app-bar',
  data: () => ({
    categories: [
      {
        id: 1,
        title: 'Iklan Tawar Bersama',
        route: '/iklantb',
      },
      {
        id: 2,
        title: 'Iklan Baris',
        route: '/kategori-ib',
      },
      {
        id: 4,
        title: 'Aksesoris & Suku Cadang',
        route: '/aksesoris-sparepart',
      },
      { id: 3, title: 'Tiket Tawar Bersama', route: '/ticket' },
       { id: 5, title: 'Cek Harga Pasar', route: '/harga-pasar' },
    ],
    jual: [
      {
        id: 1,
        title: 'Tambah Unit',
        route: '/garage/add-unit',
      },
      {
        id: 2,
        title: 'Tambah Iklan',
        route: '/seller/add',
      },
    ],
    keyword: '',
  }),
  computed: {
    ...mapGetters({
      guest: 'auth/guest',
      user: 'auth/user',
    }),
    isHome() {
      return this.$route.path === '/'
    },
  },
  methods: {
    doSearch() {
      this.$refs.childComponent.doSearch()
    },
    go() {
      this.$refs.childComponent.hasilPencarian()
    },
  },
}
</script>