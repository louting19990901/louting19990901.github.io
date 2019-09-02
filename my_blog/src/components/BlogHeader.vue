<template>
  <nav>
    <li>
      <router-link to="/" exact>看博客</router-link>
      <router-link to="/addblog" exact>写博客</router-link>
    </li>
  </nav>
</template>


<script></script>
export default {
  name:"blog-header"
}
</script>

<style scoped>
ul {
  list-style-type: none;
  text-align: center;
  margin: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #fff;
  text-decoration: none;
  padding: 12px;
  border-radius: 5px;
}
nav {
  background: skyblue;
  padding: 30px 0;
  margin-bottom: 40px;
}
.router-link-active {
  background: rgb(255, 255, 255, 0.8);
  color: #444;
}
</style>