<template>
  <div id="app">
    <v-app dark>
      <v-navigation-drawer
        persistent
        v-model="drawer"
        app
      >
      </v-navigation-drawer>
      <v-toolbar fixed app color="grey darken-4" dark>
        <v-toolbar-side-icon @click.native.stop="drawer = !drawer"></v-toolbar-side-icon>
        <v-btn
          icon
        >
          <v-icon>palette</v-icon>
        </v-btn>
        <v-toolbar-title v-text="title"></v-toolbar-title>
      </v-toolbar>
      <main>
        <v-content>
          <v-container fluid fill-height>
            <welcome-view></welcome-view>
          </v-container>
        </v-content>
      </main>
      <v-footer :fixed="fixed" app>
        <v-spacer></v-spacer>
        <span>&copy; 2017</span>
      </v-footer>
    </v-app>
  </div>
</template>

<script>
  import WelcomeView from '@/components/WelcomeView'
  export default {
    name: 'experiment',
    components: {
      WelcomeView
    },
    data: () => ({
      drawer: false,
      fixed: false,
      title: 'Picka'
    })
  }
</script>

<style lang="stylus">
  @import './assets/stylus/main.styl'
</style>


<style>
  @import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons');
  /* Global CSS */
</style>
