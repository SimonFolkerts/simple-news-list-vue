<template>
  <div>
    <SourceSelection v-on:$sourceChanged="sourceChanged" />
    <NewsList v-bind:source="source" />
  </div>
</template>

<script>
import SourceSelection from "./SourceSelection";
import NewsList from "./NewsList";

export default {
  name: "Home",
  data: function() {
    return {
      source: ""
    };
  },
  components: {
    SourceSelection,
    NewsList
  },
  methods: {
    sourceChanged: function(source) {
      this.source = source;
    }
  }
};
</script>

<style scoped></style>
