<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ this.article.title }}</h5>
      <p class="card-text">{{ this.article.description }}</p>
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">
        <span v-for="topic in topics" :key="topic.name">
          <span class="badge badge-secondary">{{ topic.name }}</span>
        </span>
      </li>
      <li class="list-group-item">{{ this.article.authors }}</li>
      <li class="list-group-item">{{ this.article.datePublished }}</li>
    </ul>
    <div class="card-body">
      <a :href="this.article.link" target="_blank" class="card-link">View</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Article",
  props: {
    article: Object
  },
  data: function() {
    return {
      topics: null
    };
  },
  created() {
    this.topics = this.article.topics;
  }
  //   created() {
  //     let polyfillScript = document.createElement("script");
  //     polyfillScript.setAttribute("src", "https://polyfill.io/v3/polyfill.min.js?features=es6");
  //     document.head.appendChild(polyfillScript);
  //     let mathjaxScript = document.createElement("script");
  //     mathjaxScript.setAttribute("src", "https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js");
  //     document.head.appendChild(mathjaxScript);
  //   }
};
</script>

<style scoped>
.card-body {
  min-width: 300px;
  margin-right: 5px;
}
.card-body .card-text {
  height: 100px;
}
.card-title {
  height: 7rem;
  /* -webkit-line-clamp: 4; */
}
.badge {
  margin-right: 5px;
}
</style>