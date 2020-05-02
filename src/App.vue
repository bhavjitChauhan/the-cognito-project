<template>
  <div id="app">
    <div class="container">
      <h1>Cognito</h1>
      <Search @newResult="addResult" @newArticle="addArticle" @clear="clear" />
      <div id="results-container">
        <hr />
        <h2>Results</h2>
        <div id="results" v-for="result in results" :key="result.source">
          <Result v-bind:result="result" />
        </div>
      </div>
      <div id="articles-container">
        <hr />
        <h2>Articles</h2>
        <div class="container-fluid py-2 overflow-auto">
          <div class="d-flex flex-row flex-nowrap card-group">
            <div id="articles" v-for="article in articles" :key="article.title">
              <Article v-bind:article="article" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Result from "./components/Result.vue";
import Article from "./components/Article.vue";

export default {
  name: "App",
  data: function() {
    return {
      results: [
        {
          source: "Example",
          description: "Example text."
        }
      ],
      articles: [
        {
          title: "Example 1",
          description: "Example text.",
          topics: [
            {
              name: "test"
            }
          ]
        },
        {
          title: "Example 2",
          description: "Example text."
        },
        {
          title: "Example 3",
          description: "Example text."
        }
      ]
    };
  },
  methods: {
    addResult: function(object) {
      console.log(`Adding result ${object.source}...`);
      setTimeout(this.results.push(object), 3000);
      // console.debug(this.results);
    },
    // updateResult: function(source, object) {
    //   console.log(`Updating result ${source}...`);
    //   let index = this.results.map(entry => entry.source).indexOf(source);
    //   this.results[index] = Object.assign({}, this.resluts[index], object);
    //   // console.debug(this.results);
    // },
    addArticle: function(object) {
      console.log(`Adding article ${object.title}...`);
      setTimeout(this.articles.push(object), 3000);
      // console.debug(this.articles);
    },
    clear: function() {
      this.results = [];
      this.articles = [];
    }
  },
  components: {
    Search,
    Result,
    Article
  },
  updated() {
    if (this.results.length !== 0) {
      document.getElementById("results-container").style.display = "block";
    } else {
      document.getElementById("results-container").style.display = "none";
    }
    if (this.articles.length !== 0) {
      document.getElementById("articles-container").style.display = "block";
    } else {
      document.getElementById("articles-container").style.display = "none";
    }
  }
};
</script>

<style>
h1 {
  text-align: center;
  padding-bottom: 50px;
}
.scrolling-wrapper {
  -webkit-overflow-scrolling: touch;
}
#app {
  padding-top: 5%;
  padding-bottom: 10%;
}
#results-container {
  /* display: none; */
  padding-top: 10px;
}
#results {
  padding-top: 25px;
}
#article-container {
  /* display: none; */
  padding-top: 10px;
}
</style>
