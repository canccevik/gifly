<template>
    <div class="gif-container">
        <p class="loadingText" v-if="loading">Loading...</p>
        <div v-if="!loading">
            <h2>{{title}}</h2>
            <div class="gifs" v-bind:class="[direction, direction == 'horizontal' ? 'flex-start' : 'flex-center']">
                <div class="gif" v-bind:key="gif" v-for="(gif, index) in gifs">
                    <a v-bind:href="gif.url" target="blank">
                        <img v-bind:style="{ background: imageValues[index].color }" v-bind:width="imageValues[index].width" v-bind:height="imageValues[index].height" v-bind:src="gif.images.fixed_height.url">
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Gifs",
    props: {
        title: { type: String, required: true },
        query: { type: String, required: true },
        count: { type: Number, required: true, default: 1 },
        direction: {type: String, default: "horizontal"}
    },
    data() {
        return {
            loading: true,
            gifs: [],
            imageValues: [],
        }
    },
    created() {
        this.getData();
    },
    methods: {
        async getData() {
            let query = "https://api.giphy.com/v1/gifs/" + this.query + (this.query.includes("?") ? "&" : "?") + "api_key=TVfqsFqwqaYw6I91MHVyQGs1OOhdmigO";
            for (let i = 0; i < this.count; i++) {
                let result = await fetch(query)
                .then(res => res.json());

                if (this.count == "25")
                {
                    this.gifs.push(result.data);
                    this.imageValues.push({
                        width: result.data.images.fixed_height.width,
                        height: result.data.images.fixed_height.height,
                        color: this.getRandomColor()
                    });
                }
                else
                {
                    this.gifs = result.data;
                    let pageCount = Math.floor(result.pagination.total_count / result.pagination.count);
                    this.$emit("page-count", pageCount);

                    for (let k = 0; k < result.pagination.count; k++) {
                        this.imageValues.push({
                            width: result.data[k].images.fixed_height.width,
                            height: result.data[k].images.fixed_height.height,
                            color: this.getRandomColor()
                        });
                    }
                }
            }
            this.loading = false;
        },
        getRandomColor() {
            let colors = ["#00ccff", "#00ff99", "#9933ff", "#d4ca4e", "#6057fe", "#e746b6", "#ff6766"];
            let color = colors[Math.floor(Math.random() * colors.length)];
            return color;
        },
    },
    watch: {
        query: function() {
            this.getData();
        }
    }
}
</script>

<style>
    .gif-container {
        padding: 15px 0;
    }

    .gifs {
        width: 100%;
        display: flex;
        padding: 10px 0;
    }

    .gif {
        margin-right: 10px;
    }

    .loadingText {
        text-align: center;
    }
    
    .horizontal {
        flex-wrap: nowrap;
        overflow-x: scroll;
    }

    .vertical {
        flex-wrap: wrap;
        overflow-x: unset;
    }

    .flex-center {
        justify-content: center;
    }

    .flex-start {
        justify-content: flex-start;
    }
</style>