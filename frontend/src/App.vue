<template>
  <div id="app">
    <header class="blog-header__container">
      <div class="blog-header__wrapper">
        <router-link to="/">
          <h1 class="blog_title">Demo Blog</h1>
        </router-link>
      </div>
    </header>
    <div class="contents-container">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

* {
  margin: 0;
  padding: 0;
}

.blog-header__container {
  position: fixed;
  display: flex;
  justify-content: center;
  z-index: 1000;
  width: 100%;
  background-color: #fff;
  top: 0;
  border-bottom: 1px solid #e3e3e3;
}

.blog-header__wrapper {
  width: calc(100% - 100px);
  padding: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 83px;
  width: 100%;
  max-width: 1170px;
  margin: 0 auto;
}

.contents-container {
  max-width: 1170px;
  margin: auto;
  padding-top: 110px;
}

a,
a:link,
a:visited {
  color: #3e414d;
  text-decoration: none;
}

a.hover {
  content: "";
  width: 0;
  height: 1px;
  display: block;
  transition: 0.3s;
}

.blog_title,
.blog_title:visited {
  color: #3e414d;
}
</style>
