<template>
  <div class="article">
    <h1>{{article.Title}}</h1>
    <h2>{{article.Description}}</h2>
    <p><router-link to="/">Homeへ</router-link></p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Article',
  data () {
    return {
      // createdでデータを取得したデータを入れてくれるので一旦null
      article: ''
    }
  },
  created () {
    // urlで指定された動的パラメーターから商品情報をとってくる。
    axios.get(`http://localhost:8080/api/v1/articles/${this.$route.params.id}`).then(res => {
      this.article = res.data
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
a {
  color: #42b983;
}
</style>
