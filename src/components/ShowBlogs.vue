<template>
    <div id="show-blogs">
      <h1>博客总览</h1>
      <input type="text" v-model="search" placeholder="搜索">

      <div v-for="blog in blogs" class="single-blog">
        <router-link :to="{path:'/info',query:{id:blog.blogId}}">
            <h2 v-rainbow>{{blog.title}}</h2>
        </router-link>

        <article>
          {{blog.content | snippet}}
        </article>
      </div>
    </div>
</template>

<script>
  import axios from 'axios'
    export default {
      name: "show-blogs",
      data(){
          return {
            blogs:[],
            search:"",
            id:[]

          }
      },
      created(){
          axios.get('/blog/list')
            .then(function (data) {
                return data.data;
            })
            .then((data) => {
              this.blogs = data;
            })
      },

      // 彩虹字
      directives:{
          'rainbow':{
            bind(el,binding,vnode){
              el.style.color = "#" + Math.random().toString(16).slice(2,8);
            }
          }
      }
    }
</script>

<style scoped>
#show-blogs{
  max-width: 800px;
  margin: 0 auto;
}
.single-blog{
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
  border: 1px dotted #aaa;
}

#show-blogs a{
  color: #444;
  text-decoration:none;
}

input[type="text"]{
  padding: 8px;
  width: 100%;
  box-sizing: border-box;

}
</style>
