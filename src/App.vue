<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.jsdelivr.net/www.jsdelivr.com/8842481ae7ab89f6a46881211e6652b7f1647efd/img/logo-horizontal.svg"
          transition="scale-transition"
        />
      </div>
    </v-app-bar>

    <v-content>
      <MainApp/>
    </v-content>
    <Footer/>
  </v-app>
</template>

<script>
import MainApp from './components/MainApp';
import Footer from './components/Footer';

export default {
  name: 'App',

  components: {
    MainApp,
    Footer
  },
};
</script>
