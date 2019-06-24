<template xmlns:v-theme="http://www.w3.org/1999/xhtml">
  <div v-theme:column="'theme'" id="show-blogs">
    <h1>博客总览</h1>
    <input type="text" v-model="search" placeholder="搜索">
    <div v-for="blog in filteredBlogs" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id">
        <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
      </router-link>
      <router-link v-bind:to="'/blog/' + blog.id">
      <article>
        {{blog.body | snippet}}
      </article>
      </router-link>
    </div>
  </div>
</template>

<script>

    export default {
    name: 'show-blogs',
    data(){
      return{
        blogs: [],
        search:""
      }
    },
    created() {
      //请求
      this.$http.get('./../static/posts.json')
        .then(function (data) {
          //console.log(data)
          //显示的内容个数
          this.blogs = data.body.slice(0,10);
        })
    },
      computed:{
      filteredBlogs:function () {
        return this.blogs.filter((blog) =>{
          return blog.title.match(this.search)
        })
      }
      }
  }
</script>

<style>
#show-blogs{

  max-width: 800px;
  margin: 0 auto;
}

.single-blog{
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eeeeee;
  border: 1px dotted #eeeeee;
}

#show-blogs a{
  color:#444;
  text-decoration: none;
}

input[type="text"]{
  padding: 8px;
  width:100%;
  box-sizing: border-box;
}
</style>
