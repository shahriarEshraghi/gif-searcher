<template>
    <div>
        <form @submit.prevent="search">
            <label for="search">search giphy</label>
            <input
                type="text"
                id="search"
                v-model="keyword"
                placeholder="what gif do you looking for ?"
                @input="searchHandler"
            />
        </form>
        <div v-if="isLoading" :class="$style.gifLoader">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
        <!-- <span v-if="isLoading">Laoding...</span> -->
    </div>
</template>

<script>
export default {
    data() {
        return {
            keyword: '',
            isLoading: false,
            timeout: null,
        };
    },
    methods: {
        searchHandler() {
            clearTimeout(this.timeout);
            this.timeout = setTimeout(() => {
                this.search();
            }, 3000);
        },
        search() {
            this.isLoading = true;
            fetch(
                `https://api.giphy.com/v1/gifs/search?api_key=${process.env.VUE_APP_GIPHY_KEY_API}&q=${this.keyword}&limit=12`
            )
                .then((response) => response.json())
                .then((res) => {
                    console.log(res);
                    this.isLoading = false;
                    this.$emit('fetch-gifs', res.data);
                })
                .catch((err) => {
                    console.log(err);
                    this.isLoading = false;
                });
        },
    },
};
</script>

<style lang="scss" module>
@import '../assets/constants.scss';

form {
    align-items: flex-start;
    display: flex;
    flex-direction: column;
    margin-bottom: 3rem;
    padding: 0 0 0 1rem;
}

input {
    border: 2px solid $primary-font-color;
    border-radius: 4px;
    font-size: 1.2rem;
    margin-top: 0.5rem;
    outline: none;
    padding: 1rem;
    width: 85%;

    &:focus {
        border-color: $green;
    }
}

label {
    font-weight: 900;

    &::first-letter {
        color: $green;
        font-size: 1.5rem;
    }
}
.gifLoader {
    display: inline-block;
    position: absolute;
    width: 80px;
    height: 80px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    div {
        box-sizing: border-box;
        display: block;
        position: absolute;
        width: 64px;
        height: 64px;
        margin: 8px;
        border: 8px solid #223549;
        border-radius: 50%;
        animation: gifLoader-data-v-xxxxxxxx 1.2s cubic-bezier(0.5, 0, 0.5, 1)
            infinite;
        border-color: #223549 transparent transparent transparent;
        &:nth-child(1) {
            animation-delay: -0.45s;
        }
        &:nth-child(2) {
            animation-delay: -0.3s;
        }
        &:nth-child(3) {
            animation-delay: -0.15s;
        }
    }
}

@media (min-width: $screen-break-large) {
    input {
        width: 40%;
    }
}
@keyframes gifLoader-data-v-xxxxxxxx {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>
