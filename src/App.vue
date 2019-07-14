<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/pokemon_PNG92.webp">
    <h1>Pokemon's list with Vue.js</h1>
    <div class="list">
      <div class="item" v-for="item in list">
        <h3>{{item.name}}</h3>
      </div>
    </div>
  </div>
</template>

<script>
  import Axios from 'axios';

export default {
  name: 'app',
  data() {
    return {
      list: {},
      errors: [],
    }
  },
  mounted() {
    Axios.get('https://pokeapi.co/api/v2/pokemon/?limit=30')
            .then( res => {
              this.list = res.data.results;
            })
            .catch(err => {
              this.errors.push = err
            })
  }
}
</script>

<style>
#app {
  font-family: 'Ubuntu', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #35495e;
  margin-top: 60px;
  padding-left: 16px;
  padding-right: 16px;
}
  img{
    max-width: 200px;
    height: auto;
  }
  h1{
    font-weight: 600;
    font-size: 60px;
  }
  h3{
    text-transform: capitalize;
  }
  .list{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  .item{
    width: 25%;
    padding: 16px 32px;
    background: #35495e;
    color: #42b983;
    border: 3px solid #42b983;
    border-radius: 5px;
    margin-top: 8px;
    margin-bottom: 8px;
    cursor: pointer;
    transition: all .3s;
  }
  .item:hover{
    background: aliceblue;
    color: #42b983;
  }
</style>
