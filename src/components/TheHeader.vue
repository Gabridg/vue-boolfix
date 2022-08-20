<template>
    <div class="container">
        <div class="d-flex justify-content-between align-items-center">
            <h1>Boolfix</h1>
            <div>
                <input type="text" class="me-1" v-model.trim="term" @keyup.enter="emitSearch">
                <button class="btn btn-danger" @click="emitSearch">Cerca</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "TheHeader",
    data() {
        return {
            term: ''
        }
    },
    methods: {
        emitSearch() {
            this.$emit('search', this.term)
        }
    }
}
</script>

<style lang="scss" scoped>
@import'../assets/Scss/style.scss';

.container {
    border-bottom: 2px solid red;
}

h1 {
    color: #f00;
    font-weight: bold;
}
</style>