<template>
  <div v-if="author">
    <h2 class="page-title">Posts by {{ displayName }}</h2>
    <p class="page-subtitle">{{ author.bio }}</p>
    <PostList :posts="author.postSet" :showAuthor="false" />
  </div>
</template>

<script>
import gql from "graphql-tag";
import PostList from "@/components/PostList";

export default {
  name: "Author",
  components: {
    PostList,
  },
  data() {
    return {
      author: null,
    };
  },
  computed: {
    displayName() {
      return (
        (this.author.user.firstName &&
          this.author.user.lastName &&
          `${this.author.user.firstName} ${this.author.user.lastName}`) ||
        `${this.author.user.username}`
      );
    },
  },
  async created() {
    const user = await this.$apollo.query({
      query: gql`
        query ($username: String!) {
          authorByUsername(username: $username) {
            website
            bio
            user {
              firstName
              lastName
              username
            }
            postSet {
              title
              subtitle
              publishDate
              published
              metaDescription
              slug
              tags {
                name
              }
            }
          }
        }
      `,
      variables: {
        username: this.$route.params.username,
      },
    });
    this.author = user.data.authorByUsername;
  },
};
</script>

<style scoped>
.page-title,
.page-subtitle {
  color: #3e414d;
}
</style>
