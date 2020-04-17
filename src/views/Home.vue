<template>
    <div id="app">
        <img alt="Vue logo" src="../assets/logo.png">
        <h1>Pokemon's list with Vue.js</h1>
        <div class="list">

                <div class="item" v-for="(item, index) in list">
                    <router-link :to="{name: 'Pokemon', params: {name: item.name, url: item.url}}">
                    <h3>{{item.name}}</h3>
                    </router-link>
                </div>

        </div>
    </div>
</template>

<script>
    import Axios from 'axios';

    export default {
        name: 'home',
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

<style scoped>
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
        width: 33%;
    }

    a{
        display: flex;
        text-decoration: none;
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
    a:hover{
        color: #35495e;
        background: #fff;
    }
</style>
