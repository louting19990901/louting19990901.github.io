<template>
  <div id="single-blog">
    <h1 v-rainbow>{{blog.title}}</h1>
    <article>{{blog.content}}</article>
    <p>作者：{{blog.author}}</p>
    <p>分类：</p>
    <ul>
      <li v-for="category in blog.categories" :key="category">{{category}}</li>
    </ul>
    <button @click="deleteSingleBlog()">删除</button>

    <router-link :to="'/edit/'+id" type="button">编辑</router-link>
  </div>
</template>

<script>
export default {
  name: "single-blog",
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    };
  },
  created() {
    this.$http
      .get("https://my-blog-5e80a.firebaseio.com/blogs/" + this.id + ".json")
      .then(function(data) {
        // console.log(data);
        // this.blog = data.body;
        return data.json();
      })
      .then(function(data) {
        this.blog = data;
      });
  },
  methods: {
    deleteSingleBlog() {
      this.$http
        .delete(
          "https://my-blog-5e80a.firebaseio.com/blogs/" + this.id + ".json"
        )
        .then(response => {
          this.$router.push({ path: "/" });
        });
    }
  }
};
</script>

<style scoped>
#single-blog {
  max-width: 960px;
  margin: 0 auto;
  padding: 20px;
  background: #eee;
  border: 1px dotted #aaa;
}
</style>