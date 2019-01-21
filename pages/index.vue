<template>
  <section id="posts">
    <PostPreview 
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnailImage="post.thumbnailUrl"
      :id="post.id"
      />
  </section>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview";
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "blog/"
      })
      .then(res => {
        console.log(res);
        return {
          posts: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              previewText: bp.content.summary,
              thumbnailUrl: bp.content.thumbnail
            };
          })
        };
      });
  }
  // data() {
  //   return {
  //     posts: [
  //       {
  //         title: "Test post",
  //         previewText: "This will be cool, wait for it",
  //         thumbnailUrl:
  //           "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSIY5J78PoCCQcZzDFT4BQL5TWxnqaCXlvSANz2x_fKh-Jh3HkvVg",
  //         id: "test-post "
  //       },
  //       {
  //         title: "Test second",
  //         previewText: "This will be cool, wait for it",
  //         thumbnailUrl:
  //           "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSIY5J78PoCCQcZzDFT4BQL5TWxnqaCXlvSANz2x_fKh-Jh3HkvVg",
  //         id: "test-second"
  //       }
  //     ]
  //   };
  // }
};
</script>

<style scoped>
#posts {
  padding-top: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 35rem) {
  #posts {
    flex-direction: row;
  }
}
</style>
