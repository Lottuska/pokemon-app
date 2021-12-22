<template>
  <v-container fluid>
    <!-- Grid for all Pokémons -->
    <div class="grid">
      <v-card
        v-for="(pokemon, index) in pokemons"
        :key="index"
        class="ma-2 pa-0"
        @click="pokemonDetails(pokemon.id)"
      >
        <div class="pokemon-id-chip">#{{ pokemon.id }}</div>
        <div class="d-flex flex-column align-center justify-center pa-2">
          <img
            class="pokemon-image-grid"
            :src="pokemonImageURL + pokemon.id + '.png'"
            :alt="pokemon.name"
          />
          <v-card-title class="text-capitalize">
            {{ pokemon.name }}
          </v-card-title>
        </div>
      </v-card>
    </div>

    <!-- Dialog for Pokémon details -->
    <v-dialog v-model="dialog" width="500">
      <v-card>
        <!-- Toolbar for Pokémon ID and close button -->
        <v-toolbar class="fixed-bar" color="#ffffff" height="80px" flat>
          <div class="toolbar-chip">#{{ pokemonDetailId }}</div>
          <v-spacer></v-spacer>
          <v-toolbar-title class="text-capitalize">{{
            selectedPokemon.name
          }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn
            fab
            text
            @click="
              dialog = false;
              tabs = 0;
            "
          >
            <v-icon> mdi-close </v-icon>
          </v-btn>
        </v-toolbar>
        <div class="d-flex flex-column align-center justify-center">
          <img
            class="pokemon-image-details"
            :src="pokemonImageURL + pokemonDetailId + '.png'"
            :alt="selectedPokemon.name"
          />
          <!-- Pokémon types -->
          <div class="d-flex flex-row align-start pa-2">
            <v-chip
              dark
              v-for="(info, index) in selectedPokemon.types"
              :key="index"
              class="ma-1 text-uppercase"
            >
              {{ info.type.name }}
            </v-chip>
          </div>
          <!-- Tabs -->
          <v-tabs
            v-model="tabs"
            fixed-tabs
            dark
            background-color="#b43c46"
            class="rounded-t-xl"
          >
            <v-tab>Stats</v-tab>
            <v-tab>Moves</v-tab>
          </v-tabs>
          <!-- Tabs content -->
          <v-tabs-items
            v-model="tabs"
            class="tab-content pa-2 tabs-background"
            dark
          >
            <!-- Stats -->
            <v-tab-item>
              <v-simple-table class="table tabs-background text-uppercase">
                <template>
                  <tbody>
                    <tr
                      v-for="(pokemonStat, index) in selectedPokemon.stats"
                      :key="index"
                    >
                      <td>{{ pokemonStat.stat.name }}</td>
                      <td>{{ pokemonStat.base_stat }}</td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-tab-item>
            <!-- Moves -->
            <v-tab-item>
              <v-simple-table class="table tabs-background text-uppercase">
                <template>
                  <tbody>
                    <tr
                      v-for="(pokemonMove, index) in selectedPokemon.moves"
                      :key="index"
                    >
                      <td>{{ pokemonMove.move.name }}</td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-tab-item>
          </v-tabs-items>
        </div>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "Pokemons",

  data() {
    return {
      dialog: false,
      tabs: 0,
      kanto: 151,
      pokemonsURL: "https://pokeapi.co/api/v2/pokemon?limit=",
      pokemonImageURL:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/",
      // other possible image urls:
      // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{ID}.png
      // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/{ID}.png
      // https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/{ID}.png
      pokemonURL: "https://pokeapi.co/api/v2/pokemon/",
      pokemons: [],
      pokemonDetailId: "",
      selectedPokemon: [],
    };
  },
  methods: {
    pokemonDetails(id) {
      this.dialog = true; // Open dialog
      this.pokemonDetailId = id; // Use selected Pokémon's ID
      axios.get(this.pokemonURL + this.pokemonDetailId).then((response) => {
        this.selectedPokemon = response.data;
        console.log("Pokémon No. " + this.pokemonDetailId + " fetched from API");
      });
      console.log("Show details of Pokémon No. " + this.pokemonDetailId);
    },
    showPokemons() {
      if (localStorage.Pokemons) {
        // Load Pokémons from Local Storage if possible
        let localPokemons = localStorage.getItem("Pokemons");
        let obj = JSON.parse(localPokemons);
        obj.results.forEach((pokemon) => {
          this.pokemons.push(pokemon);
        });
        console.log("Pokémons loaded from Local Storage");
      } else {
        axios
          .get(this.pokemonsURL + this.kanto) // Get Pokémon API data
          .then((response) => {
            return response.data;
          })
          .then((data) => {
            data.results.forEach((pokemon) => {
              pokemon.id = pokemon.url // Get Pokémon ID from url
                .split("/")
                .filter(function (part) {
                  return !!part;
                })
                .pop();
              this.pokemons.push(pokemon);
            });
            console.log("Pokémons fetched from API");
            const pokemonJSON = JSON.stringify(data);
            localStorage.setItem("Pokemons", pokemonJSON); // Save Pokémon data to Local Storage
            console.log("Pokémons saved to Local Storage");
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
  created() {
    this.showPokemons();
  },
};
</script>

<style>
.leaflet-fade-anim .leaflet-tile,
.leaflet-zoom-anim .leaflet-zoom-animated { will-change: auto !important; }
.pokemon-image-grid {
  width: 140px;
  height: auto;
}
.pokemon-image-details {
  width: 250px;
  height: auto;
}
.tabs-background { background-color: #b43c46 !important; }
.tab-content { width: 100%; }
.fixed-bar {
  position: sticky;
  position: -webkit-sticky;
  top: 0px;
  z-index: 2;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, max-content));
  justify-content: center;
}
.table { width: 100%; }
tr:hover { background-color: transparent !important; }
.close-icon {
  position: absolute !important;
  top: 20 !important;
  right: 20 !important;
}
.pokemon-id-chip {
  background-color: #1e5397;
  color: #ffffff;
  width: 56px;
  height: 56px;
  position: absolute;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 0px 10px 10px 0px;
  border-radius: 4px 0px 60px 0px !important;
  font-size: 1em;
}
.toolbar-chip {
  background-color: #b43c46;
  color: #ffffff;
  width: 56px;
  height: 56px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  font-size: 1.2em;
}
@media (max-width: 430px) {
  .grid {
    grid-template-columns: repeat(auto-fit, minmax(50%, max-content));
  }
}
@media (max-width: 330px) {
  .pokemon-image-grid,
  .pokemon-image-details {
    width: 100%;
  }
  .grid {
    grid-template-columns: repeat(auto-fit, minmax(100%, max-content));
  }
}
</style>
