<template>
  <div>
    <input type="search" v-model="query" />
    <button @click="search">Search</button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data: function() {
    return {
      query: ""
    };
  },
  methods: {
    // This is not the final method, just for testing
    search: function() {
      let callback = (source, data) => {
        this.$emit("input", {
          source: source,
          data: data
        });
      };

      this.$emit("clear");

      let query = this.query;
      var request = new XMLHttpRequest();
      var url = "https://en.wikipedia.org/w/api.php";
      let data;
      // A cleaner method of passing parameters
      var params = {
        action: "query",
        format: "json",
        prop: "pageimages%7Cpageterms&",
        generator: "prefixsearch",
        redirects: 1,
        piprop: "thumbnail",
        pithumbsize: 250,
        pilimit: 20,
        wbptterms: "description",
        gpssearch: query
      };
      // Append parameters to the end of the URL
      url = url + "?origin=*";
      Object.keys(params).forEach(function(key) {
        url += "&" + key + "=" + params[key];
      });

      request.open("GET", url, true);

      request.onload = function() {
        if (this.status >= 200 && this.status < 400) {
          // Success!
          data = JSON.parse(this.response);
          console.log(
            data.query.pages[Object.keys(data.query.pages)[0]].terms.description
          );
          data =
            data.query.pages[Object.keys(data.query.pages)[0]].terms
              .description[0];
          callback("wikipedia", data);
        } else {
          // We reached our target server, but it returned an error
          console.error(`Server error for ${query}.`);
        }
      };

      request.onerror = function() {
        // There was a connection error of some sort
        console.error(`Connection error for ${query}.`);
      };

      request.send();
    }
  }
};
</script>

<style scoped>
</style>
