<template>
  <div id="app">
    <h1>Cognito</h1>
    <Search @input="addResult" @update="updateResult" @clear="clear" />
    <div id="results" v-for="result in results" :key="result.source">
      <Result v-bind:result="result" />
    </div>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  data: function() {
    return {
      results: [
        {
          source: "Example",
          data: "Example text."
        }
      ]
    };
  },
  methods: {
    addResult: function(object) {
      console.log(`Adding result ${object.source}...`);
      setTimeout(this.results.push(object), 3000);
      console.debug(this.results);
    },
    updateResult: function(source, object) {
      console.log(`Updating result ${source}...`);
      let index = this.results.map(entry => entry.source).indexOf(source);
      this.results[index] = Object.assign({}, this.resluts[index], object);
      console.debug(this.results);
    },
    clear: function() {
      this.results = [];
    }
  },
  components: {
    Search,
    Result
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 25px;
  margin-top: 60px;
}
#results {
  padding-top: 25px;
}
</style>
