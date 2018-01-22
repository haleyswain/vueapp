<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent="queryGitHub(query)">
      <input type="text" placeholder="github username" v-model="query"/>
    </form>
    <div class="results" v-if="results">
      <img v-if="results.avatar_url" v-bind:src="results.avatar_url">
      <h2 v-if="results.name">{{results.name}}</h2>
      <h3 v-if="results.bio">{{results.bio}}</h3>
      <h3 v-if="results.message">User not found</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GitHub',
  data () {
    return {
      msg: 'Github search',
      query: '',
      results: null
    }
  },
  methods: {
    queryGitHub(q) {
      let self = this;
      fetch('https://api.github.com/users/' + q)
      .then((j) => {
        return j.json();
      })
      .then((r) => {
        console.log(r);
        self.results = r;
      })
    }
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
