<template>
    <div class="card-pokemon item">
      <div class="bl-info-pokemon">
        <img :src="image" v-bind:alt="`Imagen del Pokémon ${name}`">
        <div class="footer">
          <span>{{ name }}</span>
          <p>{{ number }}</p>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'CardPokemon',
  props: ['name', 'image', 'number']
}
</script>


<style>
.card-pokemon {
  border-radius: 3px;
  padding: 10px;
  /*width: 100%;*/
  height: 150px;
  background: #fff;
/*box-shadow: 0 1px 1px 0;*/
}
.bl-info-pokemon{
  /*width: 100%;*/
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
.footer{
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
span{text-transform: capitalize;}
</style>
