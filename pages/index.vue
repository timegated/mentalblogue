<template>
  <main class="posts-main">
    <h2>Posts</h2>
    <div class="post" v-for="post in posts" :key="post.id">
      <h3>
        <a :href="`blog/${post.slug}`">{{ post.title.rendered }}</a>
      </h3>
      <div v-html="post.excerpt.rendered"></div>
      <a :href="`blog/${post.slug}`" class="readmore">Read More --></a>
    </div>
  </main>
</template>

<script>
export default {
  computed: {
    posts() {
      return this.$store.state.posts;
    },
  },
  created() {
    this.$store.dispatch("getPosts");
  },
};
</script>
<style>
  .posts-main {
    padding: 10rem;
  }
  
  .post {
    border: 1px solid black;
    padding: 1.5rem;
  }
</style>