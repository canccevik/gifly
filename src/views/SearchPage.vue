<template>
  <div>
      <div class="search">
        <div class="searchBox">
          <input type="text" @keypress.enter="search()" v-model="searchingText">
        </div>
        <div class="btn-wrapper">
          <a class="btn-search" v-on:click="search()">Search</a>
        </div>
      </div>
      <TrendingSearches v-on:trending-clicked="handleTrendingClicked" />
      <Gifs title="Search results:" :query="query" v-on:page-count="handlePageCount" direction="vertical" />
      <Pagination :pageCount="isNaN(pageCount) ? 0 : pageCount" v-on:clicked="handleSelectedIndex" />
  </div>
</template>

<script>
import Gifs from "../components/Gifs";
import Pagination from "../components/Pagination";
import TrendingSearches from "../components/TrendingSearches";

export default {
    name: "Search",
    components: { Gifs, Pagination, TrendingSearches },
    data() {
      return {
        searchingText: "",
        query: "search?q=",
        pageCount: 1,
        currentPage: 1,
      }
    },
    created() {
      let initList = ["Mr. Robot", "Taylor Swift", "Batman", "Gamer", "Dogs", "City", "The Simpsons", "Netflix"];
      this.searchingText = initList[Math.floor(Math.random() * initList.length)];
      this.search();
    },
    methods: {
      search() {
        this.query = "search?q=" + this.searchingText;
      },
      handleSelectedIndex(index) {
        this.query = "search?q=" + this.searchingText + "&offset=" + ((index - 1) * 25).toString();
        this.currentPage = index;
      },
      handleTrendingClicked(value) {
        this.query = "search?q=" + value + "&offset=" + ((this.currentPage - 1) * 25).toString();
        this.searchingText = value;
        window.scrollTo(0,0);
      },
      handlePageCount(pageCount) {
        this.pageCount = pageCount;
      }
    }
}
</script>

<style>
  .search {
    width: 100%;
    background-color: black;
    padding: 5px 10px;
    display: flex;
    align-items: center;
  }

  .searchBox {
    padding: 5px;
    flex: 10;
  }

  .searchBox input {
    width: 100%;
    padding: 5px 5px;
    font-size: 20px;
  }

  .btn-wrapper {
    flex: 1;
    height: 48px;
    background-color: white;
    color: black;
    text-align: center;
    cursor: pointer;
    border: 2px solid black;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: .2s;
  }

  .btn-wrapper:hover {
    background-color: black;
    color: white;
    border: 2px solid white;
  }

  .btn-search {
    font-size: 20px;
    text-decoration: none;
    font-weight: bold;
  }
</style>