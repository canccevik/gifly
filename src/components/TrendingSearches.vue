<template>
    <div class="container">
        <h2>Trending Searches</h2>
        <div class="t-searches">
            <a class="btn" :key="search" v-for="search in trendingSearches" v-on:click="onClicked($event)">{{search}}</a>
        </div>
    </div>
</template>

<script>
export default {
    name: "TrendingSearches",
    data() {
        return {
            trendingSearches: [],
        }
    },
    async created() {
        this.trendingSearches = (await fetch("https://api.giphy.com/v1/trending/searches?api_key=TVfqsFqwqaYw6I91MHVyQGs1OOhdmigO").then(res => res.json()).then(res => res.data)).slice(0, 15);
    },
    methods: {
        onClicked(e) {
            this.$emit("trending-clicked", e.srcElement.firstChild.data);
        }
    }
}
</script>

<style>
    .container {
        margin-top: 10px;
        text-align: center;
    }
    
    .t-searches {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 10px;
    }

    .btn {
        padding: 5px 5px;
        border-radius: 10px;
        border: 2px solid black;
        font-weight: bold;
        margin: 5px;
        transition: .15;
        cursor: pointer;
    }

    .btn:hover {
        border: 2px solid black;
        background-color: black;
        color: white;
    }
</style>