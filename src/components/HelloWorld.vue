<template>
  <div class="hello">
    <c-heading>{{msg}}</c-heading>
  </div>
</template>

<script>

import { CHeading } from '@chakra-ui/vue'

export default {
  name: 'HelloWorld',
  fetched: '',
  props: ['msg'],
  components: {
    CHeading
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
