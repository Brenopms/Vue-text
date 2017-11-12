<template>
  <div id="app">
    <header>
      <h1 class="title">Text - Vue</h1>
    </header>
    <main>
      <aside class="sidebar">
        <router-link
            v-for="post in posts"
            active-class="is-active"
            class="link"
            :to="{ name: 'post', params: { id: post.id } }">
          {{post.id}}. {{post.title}}
        </router-link>
      </aside>
        <div class="content ">
          <router-view></router-view>
        </div>
    </main>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data () {
      return {
        posts: [],
        endpoint: 'https://jsonplaceholder.typicode.com/posts/',
      }
    },

    created() {
      this.getAllPosts();
    },

    methods: { 
      getAllPosts() {
        axios.get(this.endpoint)
          .then(response => {
            this.posts = response.data;
          })
          .catch(error => {
            console.log('-----error-------');
            console.log(error);
          })
      }
    }
  }
</script>

<style lang="scss">
  
  html {
    background-color:#393939;
  }
  body {
    margin: 0;
    padding: 0;
    background-color:#393939;
  }

  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #c6c6c6;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  header {
    position: fixed;
    top: 0;
    width: 100%;
    min-height: 90px;
    border-bottom: 1px solid #42b983;
    text-align: center;
  }

  main {
    display: flex;
    height: calc(100vh - 90px);
    max-width: 1200px;
    margin-top: 90px;
    margin-left: auto;
    margin-right: auto;
    overflow: hidden;
  }

  aside {
    flex: 1 0 20%;
    height: 100%;
    overflow-y: auto;
    width: 30%;
    padding: 50px 30px;
    box-sizing: border-box;
    border-right: 1px solid #42b983;
  }

  .title{
    color: white;
    padding-top: 20px;
  }
  .content {
    flex: 1 1 70%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .link {
    display: block;
    text-decoration: none;
    margin-bottom: 10px;
    color: #838383;

    &--home {
      text-transform: uppercase;
      margin-bottom: 30px;
    }

    &.is-active {
      color: #42b983;
    }
  }

  .link:hover{
    color: #efefef;
  }

::-webkit-scrollbar {
    width: 12px;
}

::-webkit-scrollbar-track {
  
    border-radius: 10px;
}
 
::-webkit-scrollbar-thumb {
    background-color: #1F1F1F;
    
}

::-webkit-scrollbar-thumb:hover {
    background-color: #42b983;
}
</style>
