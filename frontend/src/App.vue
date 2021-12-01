<template>
  <div id="app">
    <header>
      <router-link to="/">
        <h1>My Blog</h1>
      </router-link>
    </header>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  margin: 0;
  padding: 24px;
}

* + * {
  margin-top: 24px;
}

#app {
  margin: 0;
  padding: 0;
}
</style>
