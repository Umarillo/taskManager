<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'home' }"> Tasks</router-link>
    <router-link :to="{ name: 'addNewProject' }"> Add New Deadline</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped>
.main-nav {
  text-align: center;
  margin: 0 auto;
  margin-bottom: 15px;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: black;
  font-size: 25px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>
