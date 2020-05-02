<template>
  <div>
    <div class="input-group">
      <input
        type="search"
        class="form-control"
        placeholder="Search"
        aria-label="Text input with segmented dropdown button"
        v-model="query"
        v-on:keyup.enter="search"
      />
      <div class="input-group-append">
        <button type="button" class="btn btn-primary" @click="search">
          <font-awesome-icon icon="search" />
        </button>
        <!-- <button
          type="button"
          class="btn btn-secondary dropdown-toggle dropdown-toggle-split"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="sr-only">Toggle Dropdown</span>
        </button>
        <div class="dropdown-menu">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <a class="dropdown-item" href="#">Something else here</a>
          <div role="separator" class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Separated link</a>
        </div> -->
      </div>
    </div>

    <!-- <button @click="search">Search</button> -->
  </div>
</template>

<script>
// import func from "../../vue-temp/vue-editor-bridge";
export default {
  name: "Search",
  data: function() {
    return {
      query: "",
      encodedQuery: ""
    };
  },
  methods: {
    request: function(url, onload) {
      console.debug(`New request\n${url}`);
      var request = new XMLHttpRequest();
      request.open("GET", url, true);

      request.onload = function() {
        if (this.status >= 200 && this.status < 400) {
          console.debug(`Request successful\n${url}.`);
          onload(this.response);
        } else {
          // We reached our target server, but it returned an error
          console.error(`Server error for ${url}.`);
        }
      };

      request.onerror = function() {
        // There was a connection error of some sort
        console.error(`Connection error for ${url}.`);
      };

      request.send();
    },
    addResult: function(result) {
      result.description =
        result.description.charAt(0).toUpperCase() +
        result.description.slice(1);
      this.$emit("newResult", result);
    },
    addArticle: function(article) {
      this.$emit("newArticle", article);
    },
    // This is not the final method, just for testing
    search: function() {
      console.log(`Search for '${this.query}'...`);
      if (this.query.trim().length == 0) {
        console.warn("Empty search query.");
        return;
      }

      // Clear previous results
      this.$emit("clear");
      this.encodedQuery = encodeURI(this.query);

      this.requestWikipedia();
      this.requestArticlesCORE();
    },
    requestWikipedia() {
      var vm = this;

      // A cleaner method of passing parameters
      var params = {
        action: "query",
        format: "json",
        prop: "pageimages%7Cpageterms",
        generator: "prefixsearch",
        redirects: 1,
        piprop: "thumbnail",
        pithumbsize: 250,
        pilimit: 10,
        wbptterms: "description",
        gpssearch: this.encodedQuery
      };
      // Append parameters to the end of the URL
      let url = "https://en.wikipedia.org/w/api.php?origin=*";
      Object.keys(params).forEach(function(key) {
        url += "&" + key + "=" + params[key];
      });

      this.request(url, function(data) {
        data = JSON.parse(data);
        let page = data.query.pages[Object.keys(data.query.pages)[0]];
        let title = page.title;
        let description = page.terms.description[0];
        let image = Object.prototype.hasOwnProperty.call(page, "thumbnail")
          ? page.thumbnail.source
          : null;
        let link = `https://en.wikipedia.org/?curid=${page.pageid}`;
        vm.addResult({
          source: "Wikipedia",
          title: title,
          description: description,
          image: image,
          enlargedImage: image && image.replace(/\d+px/g, "4096px"),
          link: link,
          customText: `Read more at <a href="${link}" target="_blank">Wikipedia</a>.`,
          modalLink: (link += "&printable=yes")
        });
      });
    },
    requestWolframAlpha() {
      // const WolframAlphaAPI = require("wolfram-alpha-api");
      // const waApi = WolframAlphaAPI("R66A46-L3378U78JL");
      // waApi.getFull("2+2").then(console.log, console.error);
    },
    requestArticlesCORE() {
      var vm = this;
      let url = `https://core.ac.uk:443/api-v2/articles/search/${this.encodedQuery}?page=1&pageSize=5&metadata=true&fulltext=false&citations=false&similar=false&duplicate=false&urls=true&faithfulMetadata=false&apiKey=MPDxIskBEoUu6Fz7OqHr0Wlp8Z5vdAmL`;
      this.request(url, function(data) {
        data = JSON.parse(data);
        data = data.data;
        console.log(data);

        for (let entry in data) {
          entry = data[entry];

          let description = entry.description.substr(0, 100);
          description += "...";

          let authors;
          if (entry.authors.length > 2) {
            authors = entry.authors.length + " authors";
          } else {
            authors = entry.authors.join(", ");
          }

          let months = [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Noc",
            "Dec"
          ];
          let datePublished =
            months[entry.datePublished.substr(5, 2) - 1] +
            " " +
            entry.datePublished.substr(8, 2) +
            ", " +
            entry.datePublished.substr(0, 4);

          let topics = [];
          
          // for (let topic in entry.topics) {
          //   let topicName = entry.topics[topic].split(" ");
          //   if (topicName.length > 3) {
          //     topicName.slice(0, 2);
          //     topicName = topicName.push("...");
          //   }
          //   entry.topics[topic] = topicName.join(" ");
          // }

          let numberOfTopics = entry.topics.length;
          if (numberOfTopics > 3) {
            entry.topics = entry.topics.slice(0, 2);
            entry.topics.push(`and ${numberOfTopics - 3} more`);
          }
          for (let topic in entry.topics) {
            topic = entry.topics[topic];
            topic = topic.charAt(0).toUpperCase() + topic.slice(1);
            topics.push({
              name: topic
            });
          }

          vm.addArticle({
            title: entry.title,
            description: description,
            authors: authors,
            link: entry.downloadUrl,
            datePublished: datePublished,
            topics: topics
          });
        }
      });
    }
  }
};
</script>

<style scoped>
#search-form .form-control {
  padding-left: 2.375rem;
}

#search-form i {
  position: absolute;
  z-index: 2;
  display: block;
  width: 2.375rem;
  height: 2.375rem;
  line-height: 2.375rem;
  text-align: center;
  pointer-events: none;
  color: #aaa;
}
</style>
