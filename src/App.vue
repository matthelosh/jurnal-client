<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Logo"
          class="shrink mr-2"
          contain
          src="img/logo-smk.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="javascript:void(0);"
        v-show="!isAuth"
        text
        @click.stop="dlgSettings = true"
      >
        <span class="mr-2">Settings</span>
        <v-icon>mdi-settings</v-icon>
      </v-btn>

      <v-btn
        href="javascript:void(0);"
        v-show="isAuth"
        text
        @click.stop="logout()"
      >
        <span class="mr-2">Logout</span>
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-content>
    <Settings v-model="dlgSettings"></Settings>
    <v-overlay :value="overlay">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
  import Settings from './components/Settings'
  // import axios from 'axios'
export default {
  name: 'App',

  components: {
    // HelloWorld,
    Settings,
  },

  data: () => ({
    //
    // overlay: true,
    dlgSettings: false
  }),
  created() {
    this.getSekolah()
  },
  methods: {
    getSekolah() {
      // axios.get(this.$store.getters.server+'/api/sekolah')
      //       .then(function(res){
      //         var sekolah = res.data.data
      //         this.$store.dispatch('SET_SEKOLAH', sekolah)
      //       })
      this.$store.dispatch('SET_SEKOLAH', 'tes')
    },
    logout(){
      this.$store.dispatch('AUTH_LOGOUT')
      this.$router.push('/login')
    }
  },
  computed: {
    isAuth() {
      return this.$store.getters.isLoggedIn
    },
    overlay(){
      return this.$store.getters.overlay
    }
  },
  // watch: {
  //     overlay (val) {
  //       val && setTimeout(() => {
  //         this.overlay = false
  //       }, 3000)
  //     },
  //   },
};
</script>
