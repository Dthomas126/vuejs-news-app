<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-white">
      <a class="navbar-brand border-bottom" href="#">YourDailyNews</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav" v-for="(source,index) in sources" :key="index">
          <a class="nav-item nav-link" @click="viewSource(source)" href="#">{{ source }}</a>
        </div>
      </div>
    </nav>

    <section class="jumbotron">
      <div class="container">
        <h1 class="display-4">Daily News</h1>
        <p class="lead">Simple place where you can view articles from top news sources.</p>
      </div>
    </section>

    <section v-for="(article,index) in articles" :key="index">
      <card
        :image="article.urlToImage"
        :link="article.url"
        :title="article.title"
        :body="article.description"
        :category="article.source.name"
        :author="article.author"
      ></card>
    </section>

    <footer class="jumbotron m-0">
      <div class="container">
        <p>Company name.</p>
      </div>
    </footer>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import card from "./components/card.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    HelloWorld,
    card
  },
  data() {
    return {
      articles: "",
      sources: [
        "Health",
        "Business",
        "Entertainment",
        "Science",
        "Sports",
        "Technology"
      ],
      newsSource: ""
    };
  },

  mounted: function() {
    this.fetchArticles();
  },

  methods: {
    fetchArticles(source) {
      if (!source) {
        source = "business";
      }
      axios
        .get(
          "https://newsapi.org/v2/top-headlines?country=us&category=" +
            source +
            "&apiKey=46e3d27e0d0e4789b695d7134a1dd1cc"
        )
        .then(res => {
          this.articles = res.data.articles;
        })
        .catch(err => {
          console.log(err);
        });
    },
    viewSource(source) {
      this.fetchArticles(source);
    }
  }
};
</script>

<style>
</style>
