<template>
    <figure>
        <img :src="gif.images.original.url" />
        <figcaption>
            Embed URl is
            <input :value="gif.embed_url" type="text" readonly ref="url" />
        </figcaption>
        <button @click="copyUrlHandler">copy</button>
    </figure>
</template>

<script>
export default {
    props: {
        gif: Object,
    },
    methods: {
        copyUrlHandler() {
            this.$refs.url.select();
            document.execCommand('copy');
        },
    },
};
</script>

<style lang="scss" scoped>
@import '../assets/constants.scss';

figure {
    display: flex;
    flex-direction: column;
    margin: 1rem;
    padding: 0;

    img {
        height: 200px;
    }

    figcaption {
        color: $purple;
        margin: 0.4rem 0;
        overflow-x: auto;

        input {
            color: $primary-font-color;
            margin: 0.3rem 0;
        }
    }
}

button {
    background: transparent;
    border: 1.5px solid $green;
    border-radius: 4px;
    font-weight: bold;
    margin-top: 0.5rem;
    outline: none;
    padding: 0.5rem 1rem;
    text-transform: uppercase;
    transition: all 0.2s;

    &:hover {
        background: $green;
        color: white;
    }
}
</style>
