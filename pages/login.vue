<template>
  <div>
    <!-- <app-bar /> -->
    <div class="login-content">
      <v-container>
        <!-- -----------------------------------------------
            Start Ui Form
        ----------------------------------------------- -->
        <v-row justify="center">
          <v-col cols="12" sm="10" md="9" lg="7">
            <div class="text-center">
              <h2 class="ui-title font-weight-bold">Login</h2>
            </div>
          </v-col>
        </v-row>

        <!-- -----------------------------------------------
            End Ui Form
        ----------------------------------------------- -->
      </v-container>
    </div>
    <div>
      <v-container>
        <v-row justify="center">
          <v-col cols="9" sm="7" md="6" lg="4">
            <v-card>
              <v-card-text>
                <v-text-field
                  label="Email"
                  type="email"
                  name="email"
                  v-model="email"
                  placeholder="Email address"
                ></v-text-field>
                <v-text-field
                  v-model="password"
                  :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                  :rules="[rules.required, rules.min]"
                  :type="show1 ? 'text' : 'password'"
                  name="input-10-1"
                  label="Password"
                  placeholder="Enter password"
                  counter
                  @click:append="show1 = !show1"
                ></v-text-field>
                
                <!-- <v-checkbox
                  v-model="checkbox2"
                  class="mt-2"
                  label="Remember me"
                  hide-details
                ></v-checkbox> -->
                <div class="mt-10 text-center">
                  <v-btn type="sumbit" color="#03045E" @click.prevent="login" elevation="0" class="mr-2" style="color: white; font-size: 16px;">Login</v-btn>
                </div>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>
<script>
export default {

  name: "UiForm",
  components: {
    AppBar: () =>
      import(/* webpackChunkName: "app-bar" */ '@/components/AppBar.vue'),
       Footer: () =>
      import(/* webpackChunkName: "footer" */ '@/components/Footer.vue'),
  },
  data() {
    return {
        email: "",
        password: "",
        show1: false,
        show2: false,
        checkbox2: false,
        rules: {
            required: (value) => !!value || "Required.",
            min: (v) => v.length >= 8 || "Min 8 characters",
            emailMatch: () => "The email and password you entered don't match",
        },
    };
  },
  methods: {
    async login() {
      let formData = new FormData()

      formData.append('email', this.email)
      formData.append('password', this.password)

      await this.$axios
        .post('/login', formData)
        .then((response) => {
          
            console.log('sudah login')
        })
        .catch((error) => {
          let responses = error.response.data
          this.setAlert({
            status: true,
            color: 'error',
            text: responses.api_message,
          })
        })
    },
  },
};
</script>
