<template>
    <section>
        <Gif-display v-for="gif in gifs" :key="gif.id" :gif="gif" />
    </section>
</template>

<script>
import GifDisplay from './GifDisplay';
export default {
    components: { GifDisplay },
    props: {
        gifs: Array,
    },
};
</script>

<style lang="scss" scoped>
@import '../assets/constants.scss';

section {
    align-items: flex-start;
    border-bottom: $border-purple;
    border-top: $border-purple;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 100%;

    figure {
        width: 40%;
    }
}

@media (min-width: $screen-break-large) {
    section {
        figure {
            width: 20%;
        }
    }
}
</style>
