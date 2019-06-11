<template>
  <section class="container my-4">
    <div class="card">
      <img :src="image" class="card-image-top img-fluid" v-if="image" alt="Image">
      <div class="card-body">
        <h5 class="card-title">{{title}}</h5>
        <p class="card-text" v-if="author">
          <b>{{author}}</b>
        </p>
        <p v-if="category" class>{{category}}</p>
        <p class="card-text">{{body}}</p>
        <a v-if="link" :href="link">Continue reading</a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "card",
  props: {
    image: String,
    title: String,
    body: String,
    author: String,
    category: String,
    link: String
  }
};
</script>

<style>
</style>

