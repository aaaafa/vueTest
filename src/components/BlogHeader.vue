<template>
  <nav>
    <ul>
      <li>
        <router-link to="/" exact>博客</router-link>
        <router-link to="/add" exact>写博客</router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
  export  default {
    name:"blog-header"
  }
</script>

<style scoped>
template{

}
ul{
  list-style-type: none;
  text-align: center;
  margin: 0;
}
li{
  display: inline-block;
  margin: 0 10px;
}
a{
  color: #3e3e3e;
  text-decoration: none;
  padding: 12px;
  border-radius: 10px;
}
nav{
  max-width: 840px;
  background: #904853;
  padding: 30px 0;
  margin: auto;
  margin-bottom: 40px;
}
.router-link-active{
  background: #708080;
  color: #fff;
}
</style>
