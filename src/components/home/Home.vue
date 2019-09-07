<template>
  <div >
    <h1 class="titulo">{{ titulo }}</h1>
    <p v-show="mensagem" class="centralizado">{{ mensagem }}</p>
    <input type="seach" class="filtro" @input="filtro = $event.target.value" placehold="filtre por parte do titulo" >

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" v-bind:key="foto._id">
        <meu-painel :titulo="foto.titulo">
             <imagem-responsiva v-meu-transform:scale.animation="1.5" :url="foto.url" :titulo="foto.titulo"/>
             <meu-botao 
                rotulo="remover" 
                tipo="button" 
                :confirmacao="true" 
                @botaoAtivado="remove(foto)"
                estilo="perigo"/>
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue'
import Botao from '../shared/botao/Botao.vue';
export default {
    
  components:{
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
     'meu-botao': Botao
  },
  methods: {

    remove(foto) {
       this.$http.delete(`http://localhost:3000/v1/fotos/${foto._id}`)
            .then(() => {
               let indice = this.fotos.indexOf(foto);
               this.fotos.splice(indice, 1);
               this.mensagem = 'Foto removida com sucesso!';
               },
            erro => {
              console.log(erro);
              this.mensagem = "Não foi possivel remover a foto.";
            } )
    }
  },
 data(){
   return{
     titulo: 'Sistema Carregamento de Imagem Vue JS',
     fotos: [],
     filtro: '',
     mensagem: ''
   }
 },

 computed:{
   fotosComFiltro(){
     if(this.filtro){
       //filtrar as fotos
       let exp = new RegExp(this.filtro.trim(),'i');
       return this.fotos.filter(foto => exp.test(foto.titulo));
     }else{
       return this.fotos;
     }
   }

 },

 created(){
   this.$http.get('http://localhost:3000/v1/fotos')
    .then(res => res.json())
    .then(fotos => this.fotos = fotos,err => console.log(err));
 }
}
</script>

<style>
.titulo {
    text-align: center;
  }

  .centralizado {
    text-align: center;
  }

  
  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

 

  .filtro {
    display: block;
    width: 100%;
  }
  
</style>
