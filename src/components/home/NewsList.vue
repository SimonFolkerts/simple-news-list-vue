<template>
  <div class="container">
    <ul>
      <li class="media" v-for="article in articles" v-bind:key="article.id">
        <div class="media-left">
          <a v-bind:href="article.url" target="_blank">
            <img
              class="media-object"
              v-bind:src="article.urlToImage"
              v-bind:alt="article.title"
            />
          </a>
        </div>
        <div class="media-body">
          <h4 class="media-heading">
            <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
          </h4>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "NewsList",
  props: ["source"],
  data: function() {
    return {
      articles: []
    };
  },
  methods: {
    getArticles: function(source) {
      if (source) {
        this.$http
          .get(
            "https://newsapi.org/v2/top-headlines?sources=" +
              source +
              "&apiKey=bd9ea595a2cf470fbf9a9f9eccfeb3f5"
          )
          .then(function(data) {
            this.articles = data.body.articles;
          });
      }
    }
  },
  watch: {
    source: function(val) {
      this.getArticles(val);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.media-object {
  width: 120px;
}
</style>
