<template>
  <div>
    <div class="post-list">
      <div class="post" v-for="post in publishedPosts" :key="post.title">
        <div class="top-section">
          <div class="post__title-container">
            <router-link class="post__title" :to="`/post/${post.slug}`"
              >{{ post.title }}: {{ post.subtitle }}</router-link
            >
          </div>
          <div class="post__details">
            <span v-if="showAuthor">
              By <AuthorLink class="author__link" :author="post.author" /> on
            </span>
            <span>{{ displayableDate(post.publishDate) }}</span>
          </div>
          <p class="post__description">{{ post.metaDescription }}</p>
        </div>
        <div class="tags__container">
          <div class="post__tag" v-for="tag in post.tags" :key="tag.name">
            <router-link :to="`/tag/${tag.name}`">#{{ tag.name }}</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AuthorLink from "@/components/AuthorLink";

export default {
  name: "PostList",
  components: {
    AuthorLink,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
    showAuthor: {
      type: Boolean,
      required: false,
      default: true,
    },
  },
  computed: {
    publishedPosts() {
      return this.posts.filter((post) => post.published);
    },
  },
  methods: {
    displayableDate(date) {
      return new Intl.DateTimeFormat("en-UK", { dateStyle: "full" }).format(
        new Date(date)
      );
    },
  },
};
</script>

<style scoped>
.post-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-end;
  margin-top: 30px;
}

.post {
  width: 48%;
  border: 1px solid rgba(204, 204, 204, 0.726);
  box-shadow: 0 5px 50px 14px hsla(0, 0%, 69.8%, 0.13333);
  border-radius: 7px;
  padding: 30px 25px;
  margin-bottom: 16px;
  align-self: stretch;
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}

.post__title {
  color: #3e414d;
  font-size: 20px;
  margin-bottom: 5px;
  display: inline-block;
  text-decoration: unset;
}

.post__title::after {
  content: "";
  width: 0;
  height: 1px;
  display: block;
  background: #3e414d;
  transition: 300ms;
}

.post__title:hover::after {
  width: 100%;
}

.post__details {
  color: #3e414d;
}

.author__link {
  color: #3e414d;
  margin-bottom: 15px;
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

.post__description {
  margin-top: 10px;
  color: rgb(71, 71, 71);
  font-style: italic;
}

.tags__container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  margin-top: 20px;
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
