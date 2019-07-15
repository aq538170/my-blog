<template>
    <div id="add-blog">
      <h2>添加博客</h2>
      <form v-if="!submmited">
        <label>博客标题</label>
        <input type="text" v-model="blog.title" required />

        <label>博客内容</label>
        <textarea v-model="blog.content"></textarea>

        <!-- 类型-->
        <div id="checkboxes">

          <input type="radio" value="开发" v-model="blog.category">
          <label>开发</label>
          <input type="radio" value="测试" v-model="blog.category">
          <label>测试</label>
          <input type="radio" value="考试" v-model="blog.category">
          <label>考试</label>
          <input type="radio" value="随笔" v-model="blog.category">
          <label>随笔</label>
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
        <h3>您的博客发布成功！</h3>
      </div>

      <div id="preview">
        <h3>博客总览</h3>
        <p>博客标题：{{blog.title}}</p>
        <p>博客内容：</p>
        <p>{{blog.content}}</p>
        <p>博客分类：{{blog.category}}</p>
<!--        <ul>-->
<!--          <li v-for="category in blog.categories">-->
<!--            {{category}}-->
<!--          </li>-->
<!--        </ul>-->
        <p>作者：{{blog.author}}</p>
      </div>
    </div>
</template>

<script>
  import axios from 'axios'
    export default {
        name: "add-blog",
        data(){
          return{
            blog:{
              title:"",
              content:"",
              // categories:[],
              author:"",
              category:""
            },
            authors:["无可"],
            submmited:false
          }
        },
        methods:{
          post:function () {
              axios.post('blog/save',this.blog)
                .then((data) => {
                  this.submmited = true;
                })




            // this.$http.post("blog/save",{
            //   headers:{
            //     // "Content-type":"application/json"
            //     "Content-type":"text/xml"
            //   },
            //   title:this.blog.title,
            //   content:this.blog.content,
            //   author:this.blog.author,
            //   category:this.blog.categories[0]
            // })
            //   .then(function (data) {
            //     console.log(data);
            //     this.submmited = true;
            //   })
          }
        }
    }
</script>

<style scoped>
  #add-blog *{
    box-sizing: border-box;
  }

  #add-blog{
    margin: 20px auto;
    max-width: 600px;
    padding: 20px;
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
    margin: 20px 0;
    background: green;
    color: #fff;
    border: 0;
    padding: 14px;
    border-radius: 4px;
    font-size: 18px;
    cursor: pointer;
  }

  #preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    marrgin: 30px 0;
  }

  h3{
    margin-top: 10px;
  }


</style>
