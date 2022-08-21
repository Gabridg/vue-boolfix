<template>
    <ul>
        <li class="text-center"> <img :src="posterSrc" alt="copertina film"></li>
        <li>Titolo: {{ production.title || production.name }}</li>
        <li>Titolo Originale: {{ production.original_title || production.original_name }}</li>
        <li class="text-center">
            <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language">
            <span v-else>{{ production.original_language }}</span>
        </li>
        <li class="text-center">Voto: {{ production.vote_average }}</li>
    </ul>
</template>

<script>
export default {
    name: 'ProductionCard',
    props: {
        production: Object,
    },
    computed: {
        hasFlag() {
            const flags = ['it', 'en'];
            return flags.includes(this.production.original_language);
        },
        flagSrc() {
            return require(`../assets/img/${this.production.original_language}.png`);
        },
        posterSrc() {
            return (`https://image.tmdb.org/t/p/w500/${this.production.poster_path}`)
        }
    }
}
</script>

<style lang="scss" scoped>
@import'../assets/Scss/style.scss';

img {
    width: 50%;
}

ul {
    list-style: none;
    color: #fff;
    font-weight: 800;
    width: 200px;
    background-color: black;
    border: 2px solid red;
    line-height: 30px;
    padding: 5px;
    margin: 10px;
}
</style>