<template>
  <div id="post" v-editable="blok">
    <div class="post-thumbnail" :style="{backgroundImage: `url(${ image })`}"></div>
    <div class="post-content">
      <h1>{{ title }}</h1>
      <p>{{ content }}</p>
    </div>
  </div>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get(`cdn/stories/blog/${context.params.postId}`, {
        //to ways of checking development mode - context (if avaiable) or process.env
        version: process.env.NODE_ENV == "production" ? "published" : "draft"
      })
      .then(res => {
        return {
          blok: res.data.story.content,
          image: res.data.story.content.thumbnail,
          title: res.data.story.content.title,
          content: res.data.story.content.content
        };
      });
  },
  mounted() {
    this.$storybridge.on(["input", "published", "change"], event => {
      window.location.reload();
    });
  }
};
</script>

<style scoped>
.post-thumbnail {
  width: 100%;
  height: 300px;
  background-size: cover;
  background-position: center;
}
.post-content {
  width: 80%;
  max-width: 500px;
  margin: auto;
}

.post-content {
  white-space: pre-line;
}
</style>
