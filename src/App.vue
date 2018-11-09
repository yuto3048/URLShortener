<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h2>URL Shortener</h2>
    <form @submit.prevent="doSubmit">
        <input v-model="url" placeholder="URL">
        <button type="submit">Submit</button>
    </form>
    <p>URL is: {{ url }}</p>
    <p>shorted URL is: {{ surl }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  methods: {
    doSubmit: function(){
      axios.get('http://localhost:8080/json?url=' + this.url).then(response => {
        if (response.status === 200) {
          console.log(response)
          console.log(response.data)
          console.log(response.data.url)

          this.surl = response.data.url
        }
      })
    }
  },
  data () {
    return {
      msg: 'Welcome to URL Shortener',
      url: '',
      surl: ''
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
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

a {
  color: #42b983;
}
</style>
