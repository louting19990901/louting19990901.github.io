<template>
  <div id="add-blog">
    <h2>添加我的博客</h2>
    <form v-if="!submitted">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required />

      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>
      <div id="checkboxes">
        <label>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories" />
        <label>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories" />
        <label>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories" />
        <label>Angular4</label>
        <input type="checkbox" value="Angular4" v-model="blog.categories" />
      </div>
      <label>作者：</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author.name">{{author}}</option>
      </select>
      <button @click.prevent="post">上传到我的博客</button>
    </form>

    <div v-if="submitted">
      <h3>Congratulation!博客发布成功!</h3>
    </div>

    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：{{blog.content}}</p>
      <p>博客分类：</p>
      <ul>
        <li v-for="category in blog.categories" :key="category.id">{{category}}</li>
      </ul>
      <p>作者：{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-blog",
  methods: {
    post: function() {
      this.$http
        .post("https://my-blog-5e80a.firebaseio.com/blogs.json", this.blog)
        .then(function(data) {
          console.log(data);
          this.submitted = true;
        });
    }
  },
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: ""
      },
      authors: ["Tim", "、走险", "无烬", "娄挺", "倞倞", "shytl1"],
      submitted: false
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog * {
  box-sizing: border-box;
}
#add-blog {
  text-align: center;
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea,
select {
  display: block;
  width: 100%;
  padding: 8px;
}

textarea {
  height: 200px;
}

#checkboxes label {
  display: inline-block;
  margin-top: 0;
}

#checkbox input {
  display: inline_block;
  margin-right: 10px;
}
button {
  display: block;
  margin: 20px auto;
  background: skyblue;
  color: #fff;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}

#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
</style>
