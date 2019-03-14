<template>
  <div id="app">
    <p v-if="isloading">Loading...</p>
    <app-search v-on:searchRequested="handleSearch"></app-search>
    <app-preview :images="images"></app-preview>
  </div>
</template>

<script>
import Search from "./components/Search";
import Preview from "./components/Preview";

export default {
  name: "app",
  data() {
    return {
      isloading: false,
      images: []
    };
  },
  components: {
    appSearch: Search,
    appPreview: Preview
  },

  methods: {
    doQuery(query) {
      if (query === "") {
        query = "lviv";
      }
      let key = ""
      this.$http
        .get(
          `https://pixabay.com/api/?key=${key}&q=${query}`
        )
        .then(res => {
          return res.json();
        })
        .then(res => {
          this.images = [];
          this.images = res.hits;
          this.isloading = false;
          console.log(this.images);
        })
        .catch(err => {});
    },
    handleSearch(query) {
      this.isloading = true;
      this.doQuery(query);
    }
  },

  created() {
    this.doQuery("");
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
