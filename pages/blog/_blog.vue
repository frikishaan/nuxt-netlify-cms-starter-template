<template>
  <div class="blog">
    <img v-bind:src="blogPost.thumbnail" class="blog__featured-img" />
    <h1 class="blog__title">{{blogPost.title}}</h1>
    <div class="blog__date">{{$moment(blogPost.date).format("MMM Do YYYY")}}</div>
    <div class="blog__body" v-html="$md.render(blogPost.body)"></div>
  </div>
</template>

<script>
export default {
  // Fetching Single BlogPost
  async asyncData({ params, payload }) {
    if (payload) return { blogPost: payload };
    else
      return {
        blogPost: await require(`~/assets/content/blog/${params.blog}.json`)
      };
  }
};
</script>

<style>
.blog {
  max-width: 800px;
  margin: 2rem auto;
}
.blog__featured-img {
  width: 100%;
  height: auto;
}
div,
h1,
img {
  margin-bottom: 1rem;
}
</style>