<template>
  <div id="single-blog">
    <h1>{{blog.title}}</h1>
    <article>{{blog.content}}</article>
    <p>作者：{{blog.author.authorName}}</p>
    <p>分类：{{blog.category[0].categoryName}}</p>
  </div>

</template>

<script>
  import axios from 'axios'
  export default {
    name: "single-blog",
    data(){
      return{
        blogId:this.$route.query.id,
        blog:{}
      }
    },
    created(){
      axios.get('/blog/' + this.blogId)
        .then((data) =>{
          console.log(data);
          this.blog = data.data;
        })
    }
  }
</script>

<style scoped>
  #single-blog{
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
    background: #eee;
    border: 1px dotted #aaa;
  }

</style>
