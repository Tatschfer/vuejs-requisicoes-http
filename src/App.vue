<template>
  <div id="app">
    <header>
      <strong>Vue Nutri</strong>
    </header>

    <div v-if="loading">
      <h3 class="loading">Carregando...</h3>
    </div>
    <article v-else v-for="item in nutri" :key="item.id" class="post">
      <strong class="titulo">{{item.titulo}}</strong>
      <img :src="item.capa"/>
      <span class="categoria">Categoria: {{item.categoria}}</span>
      <p class="subtitulo">{{item.subtitulo}}</p>
      <a class="botao" href="#">Acessar</a>
    </article>

  </div>
</template>

<script>

import api from './services/api';
export default {
  name: 'App',
  data(){
    return{
      nutri: [],
      loading: true,
    }
  },
  async created(){
    const response = await api.get('?api=posts');
    this.nutri = response.data;
    this.loading = false;
  }

}
</script>

<style scoped>

#app{
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  align-items: center;
}

header{
  font-family: sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 35px;
  width: 100%;
  height: 60px;
  background-color: #1daa7b;
  color: #fff;
  }

  .post{
    color:rgb(95, 95, 95);
    font-family: sans-serif;
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 700px;
    background-color: #fff;
    border-radius: 7px;
    margin: 8px;
    padding: 30px;
  }

  .titulo{
    color:rgb(95, 95, 95);
    text-align: center;
    font-size: 25px;
    margin-bottom: 25px;
    margin-top: 10px;
  }

  .categoria{
    padding-top: 15px;
    font-weight: bold;
  }

  img{
    border-radius: 30px;
    border: #1daa7b solid 5px;
    width: 650px;
    height: 30%;
    align-self: center;
  }

  .botao{
    width: 60px;
    height: 20px;
    background: none;
    border-radius: 5px;
    border: 2px solid #e39d4c;
    color: #e39d4c;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    font-size: 13px;
    transition: all 0.5s;
  }

  .botao:hover{
    background: #e39d4c;
    color: #fff;
  }
</style>
