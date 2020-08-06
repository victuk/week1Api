<template>
  <div class="home">
    <HelloWorld msg="Welcome To Dummy Frontend App"/>
    <fetchedDataComp />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import fetchedDataComp from '@/components/fetched-data-component.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld,
    fetchedDataComp
  }
}
</script>
