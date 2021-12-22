<template>
  <v-container>
    <v-card class="pa-2">
      <v-card-title class="wrap-text">About</v-card-title>
      <v-card-text>
        Simple Pokémon application for Kanto 151 Pokémons. Click on any Pokémon to view its details, such as statistics and movements.
        The main purpose of this project was to learn more about Vue.js development, Vuetify UI framework and fetching API with Axios.
      </v-card-text>

      <v-card-title class="wrap-text">Technologies used</v-card-title>

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            ><a href="https://pokeapi.co/">PokéAPI</a></v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            An API for Pokémons and other related information.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            ><a href="https://vuejs.org/">Vue.js</a></v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            JavaScript Framework for building user interfaces and single-page
            applications.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            ><a href="https://vuetifyjs.com/en/">Vuetify</a></v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            Material Design Framework for Vue.js.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-card-title class="wrap-text">Future improvement ideas</v-card-title>

      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-heart</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            >Add favourites</v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            Mark your favourite Pokémons and save them to Local Storage.  A new page for selected favourites.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-magnify</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            >Search</v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            Search specific Pokémon by its name or ID.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-content-save</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            >Pokémon details to Local Storage</v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            Save fetched Pokémon details to Local Storage for upcoming reviews. This would save API calls and Pokémons could be viewed on Offline mode.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

       <v-list-item>
        <v-list-item-icon>
          <v-icon>mdi-plus</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title class="wrap-text"
            >More Pokémon details</v-list-item-title
          >
          <v-list-item-subtitle class="wrap-text">
            More data for individual Pokémon detail dialogs, like evolution chains, abilities or wild encounters.
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>



    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "Info"
};
</script>

<style>
.wrap-text {
  white-space: normal;
}
</style>
