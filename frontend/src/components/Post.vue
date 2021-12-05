<template>
  <div class="post" v-if="post">
    <h2 class="blog__title">{{ post.title }}: {{ post.subtitle }}</h2>
    <div class="blog__details">
      By <AuthorLink class="author__link" :author="post.author" />
      <span> on {{ displayableDate(post.publishDate) }}</span>
    </div>
    <p class="post__description">{{ post.metaDescription }}</p>
    <article>
      {{ post.body }}
    </article>
    <div class="tags__container">
      <div class="post__tag" v-for="tag in post.tags" :key="tag.name">
        <router-link :to="`/tag/${tag.name}`">#{{ tag.name }}</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
import AuthorLink from "@/components/AuthorLink";

export default {
  name: "Post",
  components: {
    AuthorLink,
  },
  data() {
    return {
      post: null,
    };
  },
  methods: {
    displayableDate(date) {
      return new Intl.DateTimeFormat("en-US", { dateStyle: "full" }).format(
        new Date(date)
      );
    },
  },
  async created() {
    const post = await this.$apollo.query({
      query: gql`
        query ($slug: String!) {
          postBySlug(slug: $slug) {
            title
            subtitle
            publishDate
            metaDescription
            slug
            body
            author {
              user {
                username
                firstName
                lastName
              }
            }
            tags {
              name
            }
          }
        }
      `,
      variables: {
        slug: this.$route.params.slug,
      },
    });
    this.post = post.data.postBySlug;
  },
};
</script>

<style scoped>
.post {
  color: #3e414d;
}

.blog__title {
  margin-bottom: 8px;
}

.blog__details {
  margin-bottom: 30px;
}

.author__link {
  color: #3e414d;
  display: inline-block;
  text-decoration: unset;
}

.author__link::after {
  content: "";
  width: 0;
  height: 1px;
  display: block;
  background: #3e414d;
  transition: 300ms;
}

.author__link:hover::after {
  width: 100%;
}

.tags__container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  margin-top: 40px;
}

.post__tag {
  list-style: none;
  font-weight: bold;
  font-size: 14px;
  background-color: #6be2d1;
  border: 1px solid transparent;
  color: #3e414d;
  display: inline-block;
  margin-bottom: 5px;
  margin-right: 5px;
  padding: 5px 8px;
  border-radius: 4px;
  transition: background-color 0.3s, border-color 0.3s, color 0.3s;
}

.post__tag:hover {
  background-color: transparent;
  border-color: #3e414d;
  color: #3e414d;
}
</style>
