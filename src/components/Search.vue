<template>
  <div class="search">
    <h2>Type in your search term</h2>

    <form v-on:submit.prevent="getResults(query)">
      <input type="text" placeholder="type in your search" v-model="query"/>
    </form>
    <div v-if='results'>
      <div v-for ="result in results">
        <img v-bind:src="result.links[0].href" alt=""> </img>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Search',
  data () {
    return {
      msg: 'Search me...',
      query:'',
      results:''
    }
  },
  methods:{
    getResults(query){
     axios.get('https://images-api.nasa.gov/search?q='+query+'&media_type=image').then(response =>{
       console.log(response.data.collection.items);
       this.results = response.data.collection.items;
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
