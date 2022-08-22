<template>
    <ul>
        <li> <img class="poster" :src="posterSrc" alt="copertina film"></li>
        <li class="prod-info">Titolo: {{ production.title || production.name }}</li>
        <li class="prod-info">Titolo Originale: {{ production.original_title || production.original_name }}</li>
        <li class="text-center prod-info">
            <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language">
            <span v-else>{{ production.original_language }}</span>
        </li>
        <li class="text-center prod-info">
            <template v-if="voteStar > 0">
                <i v-for="vote in voteStar" :key="vote" class="fa-solid fa-star"></i>
            </template>
            <span v-else>Nessun Voto</span>
        </li>
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
        },
        voteStar() {
            return Math.ceil(this.production.vote_average / 2)
        }
    }
}
</script>

<style lang="scss" scoped>
@import'../assets/scss/style.scss';

img {
    width: 70%;
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

.poster {
    display: block;
    margin: 0 auto;
}

.prod-info {
    display: none;
}

ul:hover .prod-info {
    display: block;
}

ul:hover .poster {
    display: none;
}

.fa-star {
    color: gold;
}
</style>