<template>

  
<div>
    <v-footer class="footer">
    <v-container>
      <v-row class="py-0 py-md-15">
        <!-- -----------------------------------------------
        First Column
      ----------------------------------------------- -->
        <v-col cols="12" sm="12" md="12" lg="3" class="px-xs-0">
          <h4 class="font-weight-regular font-18">Address</h4>
          <p class="mt-10">71 Amsteroum Avenue Cronish Night, NY 35098</p>
        </v-col>
        <!-- -----------------------------------------------
        Second Column
      ----------------------------------------------- -->
        <v-col cols="12" sm="12" md="12" lg="3" class="px-xs-0">
          <h4 class="font-weight-regular font-18">Phone</h4>
          <p class="mt-10 mb-0">Reception : +205 123 4567</p>
          <p>Office : +207 235 7890</p>
        </v-col>
        <!-- -----------------------------------------------
        Third Column
      ----------------------------------------------- -->
        <v-col cols="12" sm="12" md="12" lg="3" class="px-xs-0">
          <h4 class="font-weight-regular font-18">Email</h4>
          <p class="mt-10 mb-0">
            Office : <a class="dark-link" href="/">info@wrappixel.com</a>
          </p>
          <p>
            Site :
            <a class="dark-link" href="https://www.wrappixel.com/"
              >wrappixel.com</a
            >
          </p>
        </v-col>
        <!-- -----------------------------------------------
        Fourth Column
      ----------------------------------------------- -->
        <v-col cols="12" sm="12" md="12" lg="3" class="px-xs-0">
          <h4 class="font-weight-regular font-18">Social</h4>

          <div class="social-icons mt-10">
            <a href="#">
              <i class="mdi mdi-facebook"></i>
            </a>
            <a href="#">
              <i class="mdi mdi-twitter"></i>
            </a>
            <a href="#">
              <i class="mdi mdi-google-plus"></i>
            </a>
            <a href="#">
              <i class="mdi mdi-youtube"></i>
            </a>
            <a href="#">
              <i class="mdi mdi-instagram"></i>
            </a>
          </div>
        </v-col>
      </v-row>
      <div class="footer-bottom-bar font-14">
        <div class="d-block d-md-flex align-center">
          <p>
            All Rights Reserved by
            <a href="https://www.wrappixel.com/" class="link">wrappixel.com</a>
          </p>
          <div class="ml-auto">
            <div class="d-flex align-center">
              <a href="/" class="link px-4">Terms of Use</a>
              <a href="/" class="link px-4">Legal Disclaimer</a>
              <a href="/" class="link px-4">Privacy Policy</a>
            </div>
          </div>
        </div>
      </div>
    </v-container>
  </v-footer>

</div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
import Vue from 'vue'
import VueGeolocation from 'vue-browser-geolocation'

Vue.use(VueGeolocation)

export default {
  name: 'App',
  components: {
    Alert: () =>
      import(/* webpackChunkName: "alert" */ '@/components/Alert.vue'),
  },
  data: () => ({
    mounted: false,
    notif: '',
  }),
  computed: {
    ...mapGetters({
      guest: 'auth/guest',
      user: 'auth/user',
      timezone: 'timezone/region',
      utc: 'timezone/utc',
    }),
  },
  methods: {
    ...mapActions({
      setAuth: 'auth/set',
      setAlert: 'alert/set',
      setTimezone: 'timezone/set',
    }),
    async oneSignal() {
      await this.$OneSignal.push(() => {
        this.$OneSignal.isPushNotificationsEnabled((isEnabled) => {
          if (isEnabled) {
            console.log('Push notifications are enabled!')

            this.$OneSignal.getUserId().then((userId) => {
              console.log('OneSignal User ID:', userId)
              this.notif = userId + '[web]'
            })
          } else {
            console.log('Push notifications are not enabled yet.')
          }
        })
      })
    },
    async geolocation() {
      await this.$getLocation({
        enableHighAccuracy: true,
      })
    },
  },
  created() {
    let utc = this.moment().utcOffset() / 60 - 7

    if (utc == 0) {
      this.setTimezone({
        utc: utc,
        region: 'WIB',
      })
    }
    if (utc == 1) {
      this.setTimezone({
        utc: utc,
        region: 'WITA',
      })
    }
    if (utc == 2) {
      this.setTimezone({
        utc: utc,
        region: 'WIT',
      })
    }
  },
  async mounted() {
    this.mounted = true
    await this.oneSignal()
    // await this.geolocation()
  },
}
</script>

<style>
a:link {
  text-decoration: none;
}
</style>
