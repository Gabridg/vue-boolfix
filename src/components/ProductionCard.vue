<template>
    <ul>
        <li> <img :src="movie.poster_path" alt="copertina film"></li>
        <li>{{ production.title || production.name }}</li>
        <li>{{ production.original_title || production.original_name }}</li>
        <li>
            <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language">
            <span v-else>{{ production.original_language }}</span>
        </li>
        <li>{{ production.vote_average }}</li>
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
            return require(`../assets/img/${this.production.original_language}`);
        }
    }
}

</script>

<style lang="scss" scoped>
img {
    width: 50%;
}
</style>