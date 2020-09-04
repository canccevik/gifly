<template>
  <div>
      <div class="buttons" v-if="pageCount != 0">
          <div :key="btn" v-for="btn in buttons">
              <a v-bind:class="btn.class" v-on:click="clicked($event)">{{btn.index}}</a>
          </div>
      </div>
      <div v-else>
          <h2 class="noResult">No GIFs found.</h2>
      </div>
  </div>
</template>

<script>
export default {
    name: "Pagination",
    props: {
        pageCount: { type: Number }
    },
    data() {
        return {
            buttons: [],
            indexList: [],
        }
    },
    methods: {
        clicked(e) {
            let index = Number(e.srcElement.firstChild.data);

            if (this.indexList.indexOf(index) > 4 && this.pageCount > 10)
            {
                this.enableSelectedButton(index - 1);
                if (index < this.pageCount)
                    this.changeButtonsValues(1);
            }
            else
            {
                if (this.indexList[0] != 1) this.changeButtonsValues(-1);
                this.enableSelectedButton(index);
            }

            this.$emit("clicked", index);
        },
        createButtons(count) {
            this.buttons = [];
            let buttonCount = count >= 10 ? 10 : count;

            for (let i = 1; i <= buttonCount; i++) {
                this.buttons.push({
                    index: i,
                    class: i == 1 ? "active" : "",
                });
                this.indexList.push(this.buttons[i-1].index);
            }
        },
        enableSelectedButton(index) {
            this.buttons.filter(btn => btn.class == "active")[0].class = "";
            this.buttons.filter(btn => btn.index == index)[0].class = "active";
        },
        changeButtonsValues(value)
        {
            for (let i = 0; i < 10; i++) {
                this.buttons[i].index += value;
                this.indexList[i] += value;
            }
        }
    },
    watch: {
        pageCount: function(count) {
            this.createButtons(count);
        }
    },
}
</script>

<style>
    .buttons {
        display: flex;
        justify-content: center;
    }

    .buttons a {
        padding: 5px 15px;
        margin: 5px 5px;
        background: black;
        color: white;
        border-radius: 5px;
        text-decoration: none;
        transition: .3s;
        font-weight: bold;
        cursor: pointer;
    }

    .noResult {
        text-align: center;
    }

    .buttons span:hover {
        color: #3b62d9;
    }

    .active {
        color: #3b62d9 !important;
    }

    @media only screen and (max-width: 767px) {
        .buttons {
            flex-wrap: wrap;
        }

        .buttons a {
            display: block;
        }
    }
</style>