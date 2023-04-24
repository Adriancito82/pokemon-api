<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/pikachu.png')"
          class="my-3"
          contain
          height="300"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Aplicación para consultar todos los pokemon 🐱‍🚀
        </h1>
        <input id="buscar" type="text" placeholder="Buscar Pokemon" v-model="namePokemon" @input="filter(namePokemon)">
        <v-btn>Buscar</v-btn>

        <div class="section" v-if="processed">
            <CardPokemon v-for="(obj, i) in pokemons" :key="obj.id" v-bind:number="'#' + (i + 1)"
            v-bind:name="obj.name" v-bind:image="obj.sprites.front_default" />
        </div>

        <div class="section" v-else>
            <CardPokemon v-bind:number="'#' + pokemon.id" v-bind:name="pokemon.name" v-bind:image="pokemon.sprites.front_default" />
        </div>

      </v-col>
    </v-row>
  </v-container>

</template>

<script>
import CardPokemon from '@/components/CardPokemon.vue'

export default {
    name: 'HelloWorld',
    components: {
        CardPokemon,
  },

    data: () => ({
        pokemons: [],
        namePokemon: '',
        pokemon: {},
        processed: true
    }),
    async created() {
        for (let i = 1; i < 152; i++) {
            fetch('https://pokeapi.co/api/v2/pokemon/' + i)
                .then(async response => {
                    const data = await response.json()
                this.pokemons.push(data)
                }).catch(() => {
                console.error('Hay un error!!')
            })
        }
    },
    methods: {
        filter(name) {
            let regexp = /[^a-zA-Z]/gim
            this.namePokemon = name.replace(regexp, '')

            if (name.length >= 3) {
                fetch('https://pokeapi.co/api/v2/pokemon/' + name.toLowerCase())
                    .then(async response => {
                        const data = await response.json()
                        this.pokemon = data
                    this.processed = false
                    }).catch(err => {
                    console.log(err)
                })
            }

            if (name == '') {
                document.location.reload(true)
            }
        }
  }
}
</script>

<style>
body {
    background-color: rgb(240, 240, 2);
}
input {
    margin-left: 2em;
    background-color: white;
    border: solid black 2px;
}
/*@bottom-gray: #ededed;
@color-medium-gray: #a9a9a9;*/
main {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  /*background: @bottom-gray;*/
  padding: 0 15px;
}
#campo-pesquisar {
  outline: none;
  margin: 20px 0;
  width: 100%;
  border-top: 0;
  border-left: 0;
  border-right: 0;
  border-bottom: 2px solid gray;
  background: gray;
  color: gray;
}
section{width: 100%;}
.section{
  width: 100%;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  column-gap: 10px;
  row-gap: 10px;
}
@media only screen and (max-width: 400px) {
  .section{
    grid-template-columns: 1fr;
  }
}
@media only screen and (min-width: 401px) {
  .section{
    grid-template-columns: repeat(2, 1fr);
  }
}
@media only screen and (min-width: 630px) {
  .section{
    grid-template-columns: repeat(3, 1fr);
  }
}
@media only screen and (min-width: 900px) {
  .section{
    grid-template-columns: repeat(4, 1fr);
  }
}
@media only screen and (min-width: 1257px) {
  .section{
    grid-template-columns: repeat(5, 1fr);
  }
}
@media only screen and (min-width: 1500px) {
  .section{
    grid-template-columns: repeat(6, 1fr);
  }
}
</style>
