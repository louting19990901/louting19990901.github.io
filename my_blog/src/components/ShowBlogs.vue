<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>Tim的个人博客</h1>
    <input type="text" v-model="search" placeholder="搜索" />
    <div v-for="blog in filteredBlogs" :key="blog.content" class="single-blog">
      <router-link :to="'/blog/'+blog.id">
        <h2 v-rainbow>{{blog.title |to-uppercase}}</h2>
      </router-link>
      <article>{{blog.content | snippet}}</article>
    </div>
  </div>
</template>

<script>
export default {
  name: "show-blogs",
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  created() {
    this.$http
      .get("https://my-blog-5e80a.firebaseio.com/blogs.json")
      .then(function(data) {
        return data.json();
        // console.log(data);
        this.blogs = data.body.slice(0, 10);
        // console.log(this.blogs);
      })
      .then(function(data) {
        var blogsArray = [];
        for (let key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      });
  },
  computed: {
    filteredBlogs: function() {
      return this.blogs.filter(blog => {
        return blog.title.match(this.search);
      });
    }
  },
  filters: {
    "to-uppercase": function(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
  border: 1px dotted #aaa;
}

#show-blogs a {
  color: #444;
  text-decoration: none;
}

input[type="text"] {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}
</style>
