<template>
  <section id="about-page" v-editable="blok">
    <h1>{{ title }}</h1>
    <p>
      {{content}}
    </p>
  </section>
</template>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories/about", {
        version: context.isDev ? "draft" : "published"
      })
      .then(res => {
        return {
          blok: res.data.story.content,
          title: res.data.story.content.title,
          content: res.data.story.content.content
        };
      });
  },
  // mounted() {
  //   //created is on ss, mounted is on the client side
  //   this.$storyblok.init();
  //   this.$storyblok.on("change", () => {
  //     location.reload(true);
  //   });
  // }
  mounted() {
    this.$storybridge.on(["input", "published", "change"], event => {
      // if (event.action == "input") {
      //   if (event.story.id === this.story.id) {
      //     this.story.content = event.story.content;
      //   }
      // } else {
      window.location.reload();
      // }
    });
  }
};
</script>

<style scoped>
#about-page {
  width: 80%;
  max-width: 500px;
  margin: auto;
}

#about-page p {
  white-space: pre-line;
}
</style>
