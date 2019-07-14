<template>
    <div class="pokemon">
        <router-link to="/">Back to list</router-link>
        <h1>{{name}}</h1>
        <img :src="data.sprites.front_default" alt="">
        <h3>Info</h3>
        <p>Weight: {{data.weight}}</p>
        <p>Base stat: </p>
        <ul>
            <li v-for="stat in data.stats">{{stat.stat.name}}: {{stat.base_stat}}</li>
        </ul>
        <p>Types: </p>
        <ul>
            <li v-for="type in data.types">{{type.type.name}}</li>
        </ul>
        <p>Abilities: </p>
        <ul>
            <li v-for="ability in data.abilities">{{ability.ability.name}}</li>
        </ul>
    </div>
</template>
<script>
    import Axios from 'axios';
    export default {
        name: 'pokemon',
        data() {
            return {
                name: this.$route.params.name,
                data: {},
                errors: '',
                img: '',
                url: ''
            }
        },
        mounted() {
            Axios({
                method: 'get',
                url: 'https://pokeapi.co/api/v2/pokemon/' + this.name,
            })
                .then(res => {
                    this.data = res.data;
                    this.img = res.data.sprites.front_default;
                })
                .catch(err => {
                    this.errors.push = err
                })
        }
    }
</script>
<style scoped>
    .pokemon{
        padding-left: 16px;
        padding-right: 16px;
        color: #35495e;
        text-transform: capitalize;
        font-family: 'Ubuntu', sans-serif;
    }
    h1{
        margin-top: 12px;
        margin-bottom: 16px;
    }
    h3{
        margin-top: 0;
        margin-bottom: 12px;
    }
    p{
        margin-top: 0;
        margin-bottom: 4px;
    }
    a{
        color: #fff;
        font-size: 24px;
        font-family: 'Ubuntu', sans-serif;
        text-decoration: none;
        background: #42b983;
        border: 2px solid #35495e;
        border-radius: 5px;
        padding: 3px 15px;
    }
    a:hover{

    }
</style>