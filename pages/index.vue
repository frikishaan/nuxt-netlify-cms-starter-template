<template>
  <div>
    <h1>Blog Posts</h1>
    <div class="blogs">
      <ul class="blog" v-for="blog in blogPosts" :key="blog.slug">
        <li class="blog__title">
          <nuxt-link :to="`/blog/${blog.slug}`">
            <h2>{{ blog.title }}</h2>
          </nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    blogPosts() {
      return this.$store.state.blogPosts;
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.blogs {
  max-width: 800px;
  margin: 2rem auto;
}
a {
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
</style>