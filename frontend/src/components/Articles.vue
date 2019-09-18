<template>
  <div class="Articles">
    <h1>{{ msg }}</h1>
    <ul>
      <!-- articlesの配列をループで回して取得 -->
      <li v-for="article in articles" :key="article.Id" @click="pageto(article.Id)">
        <p>{{article.Title}}</p>
      </li>
    </ul>
    <h2><router-link to="/">Homeへ</router-link></h2>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Articles',
  data () {
    return {
      msg: 'This is Articles Page',
      articles: []
    }
  },
  methods: {
    pageto: function (id) {
      this.$router.push(`/article/${id}`)
    }
  },
  created () {
    axios.get('http://localhost:8080/api/v1/articles').then(res => {
      this.articles = res.data
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
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
