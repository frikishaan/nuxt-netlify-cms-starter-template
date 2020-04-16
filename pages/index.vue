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
  data() {
    return {
      blogPosts: []
    };
  },

  // Fetching all posts
  async asyncData({ error, params, payload }) {
    if (payload) return { blogPost: payload };
    else {
      let files = await require.context(
        "~/assets/content/blog/",
        false,
        /\.json$/
      );
      let blogPosts = files.keys().map(key => {
        let res = files(key);
        res.slug = key.slice(2, -5);
        return res;
      });
      return { blogPosts };
    }
  }
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