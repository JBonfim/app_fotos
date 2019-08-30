<template>
  <div id="app">
    <h1>{{titulo}}</h1>
    <ul>
      <li  v-for="foto of fotos" v-bind:key="foto">
        <img :key="foto.titulo" :src="foto.url" :alt="foto.titulo">
      </li>
    </ul>
    
    
    
  </div>
</template>

<script>
export default {
 data(){
   return{
     titulo: 'Sistema Carregamento de Imagem',
     fotos: [
       {
        url: 'https://s2.glbimg.com/eQkhAB2FrlFSMj_Jbkw024ueqao=/e.glbimg.com/og/ed/f/original/2019/01/19/50898568_10157219683273254_5268539131058716672_o.jpg',
        titulo: 'Cachorro'
        },{
          url: 'https://s2.glbimg.com/eQkhAB2FrlFSMj_Jbkw024ueqao=/e.glbimg.com/og/ed/f/original/2019/01/19/50898568_10157219683273254_5268539131058716672_o.jpg',
          titulo: 'Cachorrao'
        }
     ]
   }
 }
}
</script>

<style>

</style>
