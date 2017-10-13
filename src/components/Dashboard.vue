<template>
        <div id='kibana' class="" >
        <iframe src="http://159.203.76.103/kibana/app/kibana#/dashboard/d54f7550-7156-11e7-8464-7d42a5464b0f?embed=true&_g=(refreshInterval%3A('%24%24hashKey'%3A'object%3A453'%2Cdisplay%3A'5%20seconds'%2Cpause%3A!f%2Csection%3A1%2Cvalue%3A5000)%2Ctime%3A(from%3Anow%2Fw%2Cmode%3Aquick%2Cto%3Anow%2Fw))" height="1100" width="100%"></iframe>

        
      </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios';
export default {
  name: 'hello',

  data: () => ({
    posts: [],
    errors: []
  }),

  methods: {
    
    },
  created() {

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
