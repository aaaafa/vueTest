<template>
  <div id="add-blog">
    <h2>添加博客</h2>
    <form v-if="!submmited">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required />

      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <label>项目</label>
        <input type="checkbox" value="项目" v-model="blog.categories">
      </div>

      <label>作者：</label>
      <select v-model="blog.author">
        <option v-for="author in authors">
          {{author}}
        </option>
      </select>
      <button v-on:click.prevent="post">添加博客</button>
    </form>

    <div v-if="submmited">
      <h3>你的博客添加成功</h3>
    </div>
    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：</p>
      <p>{{blog.content}}</p>
      <p>博客分类:</p>
      <ul>
        <li v-for="category in blog.categories">{{category}}</li>
      </ul>
      <p>作者:{{authors}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'add-blog',
    data () {
      return {
        blog:{
          title:"",
          content:"",
          categories:[],
          author:""
        },
        authors:["afa","游人"],
        submmited:false
      }
    },
    methods: {
      post: function () {
        this.$http.post("http://jsonplaceholder.typicode.com/posts", {
          title: this.blog.title,
          body: this.blog.content,
          userId: 1
        })

          .then(function (data) {
            console.log(data)
            this.submmited = true;
          })
      }
    }

  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;

}

#add-blog{
  margin:0 auto;
  max-width: 820px;
  padding: 10px;
  background: #eeeeee;
}

label{
  display: block;
  margin: 20px 0 10px;
 }

input[type="text"],textarea,select{
  display: block;
  width: 100%;
  padding: 8px;
}

textarea{
  height: 200px;
}

#checkboxes label{
  display: inline-block;
  margin-top: 0;
}

#checkboxes input{
  display: inline-block;
  margin-right: 10px;
}

button{
  display: block;
  margin:20px 0;
  background: #904853;
  color:#fff;
  border: 0;
  padding: 14px;
  border-radius: 4px ;
  font-size: 18px;
  cursor: pointer;
}

#preview{
  padding: 10px 20px;
  border: 1px dotted #cccccc;
  margin: 30px 0;
}

h3{
  margin-top: 10px;
}
</style>
