<template>
    <div class="card-pokemon item, sombra_movil">
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
  width: 100%;
  height: 150px;
  background: #fff;
  box-shadow: 0 1px 1px 0;
}
.sombra_movil{
    transform: translateX(0);
}
.sombra_movil:before{
    content: '';
    position:absolute;
    width: 90%;
    left: 5%;
    top: 100%;
    height: 10px;

    /*Primero hay que poner ellipse seguido de center, al reves no funciona*/

    background: radial-gradient(
        ellipse at center,
        rgba(0, 0, 0, 0.35) 0%,
        rgba(0, 0, 0, 0) 80%);
        transition-duration: 0.3s;
        opacity: 0;
}
.sombra_movil:hover{
    transform: translateY(-6px);
    animation: 1.5s movercaja infinite;
}
@keyframes movercaja{
    50%{
        transform: translateY(-3px);
    }
}
.sombra_movil:hover:before{
    transform: translateY(6px);
    opacity: 0.4;
    animation: 1.5s moversombra infinite;
}
@keyframes moversombra{
    50%{
        transform: translateY(3px);
        opacity: 1;
    }
}
.bl-info-pokemon{
  width: 100%;
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
