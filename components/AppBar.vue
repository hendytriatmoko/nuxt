<template>
  <div>
    <v-app-bar
      app
      class="app-header position-relative navbar-light header1"
      flat
    >
      <v-container class="py-0 fill-height">
        <!-- Logo -->
        <div class="logo">
          <NLink to="/">
            <v-img
              src="/images/logos/purple-logo.png"
              alt="logo"
            />
          </NLink>
        </div>

        <v-spacer></v-spacer>
        <v-btn class="d-block d-md-none" text @click="toggleClass()">
          <v-app-bar-nav-icon />
        </v-btn>
        <!-- Desktop view Navigation -->
        <div
          class="navigation"
          v-bind:class="[isActive ? 'd-block' : '']"
          @click="isActive = !isActive"
        >
          <ul class="navbar-nav">
            <li class="nav-item" text>
              <n-link class="nav-link" nuxt to="/"> Fitur Aplikasi </n-link>
            </li>
            <li class="nav-item" text>
              <n-link class="nav-link" nuxt to="/about"> Tentang Kami </n-link>
            </li>
            <li class="nav-item" text>
              <n-link class="nav-link" nuxt to="/work"> Work </n-link>
            </li>
            <li class="nav-item" text>
              <n-link class="nav-link" nuxt to="/services"> Harga </n-link>
            </li>
            <li class="nav-item" text>
              <n-link class="nav-link" nuxt to="/freebies"> Partner </n-link>
            </li>
          </ul>
        </div>

        <!-- login-regiter -->
        <v-btn
          class="d-none d-lg-flex btn-custom-nm ml-5"
          nuxt
          outlined
          color="primary"
          to="/login"
          elevation="0"
        >
          Login
        </v-btn>
      </v-container>
    </v-app-bar>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'app-bar',
  data: () => ({
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