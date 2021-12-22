<template>
<!-- sovelluksen runko -->
  <v-app>
    <!-- App bar -->
    <v-app-bar
      app
      color="#1e5397"
      dark
    >
    <!-- Home -->
    <router-link to="/">
      <v-btn icon title="Home" aria-label="Home">
        <v-icon>
          mdi-home
        </v-icon>
      </v-btn>
    </router-link>
    <v-toolbar-title>Pokémon</v-toolbar-title>
    <v-spacer></v-spacer>
    <!-- Site info -->
    <router-link to="/info">
      <v-btn icon title="Info" aria-label="Info">
        <v-icon>
          mdi-information
        </v-icon>
      </v-btn>
    </router-link>
    </v-app-bar>

    <!-- Content -->
    <v-main class="main-content">
      <router-view/>
    </v-main>
  
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>

<style>
.main-content {
  background-color: #e6e6e6;
}
</style>