<template>
  <div class="container">
    <div class="jumbotron">
      <h2>News List</h2>
      <h4>Select News Source</h4>
      <select v-on:change="sourceChanged">
        <option value="">Please select news source...</option>
        <option
          v-for="source in sources"
          v-bind:key="source.id"
          v-bind:value="source.id"
          >{{ source.name }}</option
        >
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "SourceSelection",
  data: function() {
    return {
      sources: []
    };
  },
  methods: {
    sourceChanged: function(evt) {
      this.$emit("$sourceChanged", evt.target.value);
    }
  },
  created: function() {
    this.$http
      .get(
        "https://newsapi.org/v2/sources?apiKey=bd9ea595a2cf470fbf9a9f9eccfeb3f5"
      )
      .then(function(data) {
        this.sources = data.body.sources;
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
