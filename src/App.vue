<template>
    <div id="app">
        <gif-searcher @fetch-gifs="onFetch" />

        <gif-list :gifs="gifs" />
    </div>
</template>

<script>
import GifSearcher from './components/GifSearcher';
import GifList from './components/GifList';

export default {
    name: 'App',
    components: {
        GifSearcher,
        GifList,
    },
    data() {
        return {
            gifs: [],
        };
    },
    methods: {
        onFetch(result) {
            this.gifs = result;
        },
    },
};
</script>

<style lang="scss">
@import './assets/constants.scss';

#app {
    color: $primary-font-color;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin-top: 60px;

    ::selection {
        background: $green-light;
    }
}

/* * * * * * */
/* Styled scroll bars */
::-webkit-scrollbar {
    width: 6px;
    height: 6px;
}

/* Track */
::-webkit-scrollbar-track {
    box-shadow: inset 0 0 5px grey;
    border-radius: 6px;
}

/* Handle */
::-webkit-scrollbar-thumb {
    background: $green;
    border-radius: 50vh;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
    background: $green-light;
}

/* * * * * * */
</style>
