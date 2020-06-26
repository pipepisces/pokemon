<template>
  <main>
    <h1>Typed Pokedex</h1>
    <div id="app">
      <div v-for="pokemon in pokemons" :key="pokemon.id" class="card">
        <span class="card-id"># {{pokemon.id}}</span>
        <img
          class="card-img"
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png`"
        />
        <h1 class="card-name">{{pokemon.name}}</h1>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      pokemons: []
    };
  },
  methods: {
    fetchData() {
      for (let i = 1; i <= 151; i++) {
        this.getPokemon(i);
      }
    },
    getPokemon(id) {
      fetch(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then(res => {
          return res.json();
        })
        .then(this.setPokemons);
    },
    setPokemons(result) {
      this.pokemons = [...this.pokemons, result];
    }
  },
  mounted() {
    this.fetchData();
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
body {
  background: #333;
  line-height: 1.5;
}
main {
  padding: 1rem;
  max-width: 1100px;
  margin: auto;
}
main > h1 {
  text-align: center;
  color: #e4c439;
  margin-bottom: 2rem;
  font-size: 2rem;
  text-transform: uppercase;
}
#app {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(12rem, 1fr));
  grid-gap: 1.5rem;
  justify-content: center;
  align-items: center;
}
.card {
  width: 12rem auto;
  background: #333;
  color: #e4c439;
  padding: 1rem;
  border-radius: 10px;
  border-top: 0.5px solid #cebf7b;
  border-bottom: 0.5px solid #cebf7b;
  text-align: center;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  position: relative;
  overflow: hidden;
  cursor: pointer;
  transition: 0.2s ease-in-out;
}
.card:hover {
  transform: scale(1.05);
}
.card-id {
  background: #cebf7b;
  width: 3rem;
  color: #333;
  padding: 0.1rem;
  font-weight: 700;
  position: absolute;
  border-radius: 0 0 10px 0;
  top: 0;
  left: 0;
}
.card-name {
  text-transform: capitalize;
  color: #fff;
  font-size: 1.5rem;
  font-weight: 700;
}
.card-img {
  width: 150px;
  display: block;
  margin: auto;
}
</style>