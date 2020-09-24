<template>
<div class="posts">
    <main class="posts-main">
    <h2>Posts</h2>
    <div class="post" v-for="post in posts" :key="post.id">
      <h3>
        <a :href="`blog/${post.slug}`">{{ post.title.rendered }}</a>
      </h3>
      <div v-html="post.excerpt.rendered"></div>
      <a :href="`blog/${post.slug}`" class="readmore slide">Read More ⟶</a>
    </div>
  </main>
</div>
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

<style lang="scss">
  .posts {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-rows: 1fr;
    grid-column-gap: 6vw;
    margin: 5rem auto;
    max-width: 80vw;
  }

  main {
    grid-area: 1 / 1 / 2 / 2;
  }

  h2 {
    margin-bottom: 2rem;
  }

  a, a:active, a:visited {
    text-decoration: none;
    color: black;
  }

  a.readmore {
    display: inline-block;
    font-size: 11px;
    text-transform: uppercase;
    padding: 5px 15px;
    letter-spacing: 2px;
    position: relative;
    color: #000;
    font-weight: 700;
    font-family: "Open Sans", sans-serif;
    border: 1px solid black;
    background: #fff;
    border-radius: 10px;
  }

  .post {
    border-bottom: 1px solid rgb(223, 222, 222);
    margin-bottom: 2rem;
    padding-bottom: 2rem;
    color: #444;
  }

  h3 {
    margin-bottom: 0.5rem;
    font-size: 26px;
  }

  .slide {
    position: relative;
    background: transparent;
    -webkit-transition: 0.3s ease;
    transition: 0.3s ease;
    z-index: 1;
    backface-visibility: hidden;
    perspective: 1000px;
    transform: translateZ(0);
    cursor: pointer;

    &:hover {
      color: #fff;
    }

    &:hover:before {
      right: -1px;
    }
  }

  .slide:before {
    content: "";
    display: block;
    position: absolute;
    background: #000;
    transition: right 0.3s ease;
    z-index: -1;
    top: -2px;
    bottom: -2px;
    left: -2px;
    right: 108%;
    backface-visibility: hidden;
    border-radius: 10px;
  }
</style>