<template>
  <div class="fetched-comp">
  <div v-for="Post in fetchedData.data" :key="Post.id">
  <c-flex bg="white" maxW="sm" rounded="sm" m="2" p="2"  style="border: 2px solid blue; border-radius: 10px;" align="center" justify="center">
    <c-text text-align="left">
    <c-box>
    <c-image :src="Post.owner.picture" :alt="Post.image" rounded="full" height="50px" width="50px" />
    <c-text justify-self="flex-start" display="inline" font-size="20px"> {{Post.owner.firstName}} </c-text>
    <c-text justify-self="flex-start" display="inline" font-size="15px" color="#C0C0C0"> {{Post.owner.email}} </c-text> <br /> <br />
     </c-box>
     <c-image :src="Post.image" :alt="Post.image" style="border-radius: 10px; text-align: center;" height="200px" width="200px" /> <br>
      {{Post.text}}
      <br />
      <c-grid template-columns="repeat(3, 1fr)" style="margin: 10px;">
  <c-box w="100%">{{Post.likes}} Likes</c-box>
  <c-box w="100%">
  <router-link :to="'/user/' + Post.owner.id">
  <c-button variant-color="blue" border="none" size="xs">
  View Profile
  </c-button>
  </router-link>
  </c-box>
  <c-box w="100%"><c-button variant-color="blue" border="none" size="xs">View Comments</c-button></c-box>
</c-grid>
<c-grid template-columns="repeat(1, 1fr)">
  <c-box w="100%">
    Tags:
  <c-grid  template-columns="repeat(4, 1fr)" v-for="(tag, index) in Post.tags" :key="index" display="inline">
  <c-text display="inline" style="background-color:#C0C0C0; color: white; padding: 3px; margin-right:4px;" border-radius="50px"> {{tag}} </c-text>
  </c-grid>
  </c-box>
</c-grid>
    </c-text>
  </c-flex>
  </div>
  </div>
</template>

<script>

import axios from 'axios'
import { CFlex, CText, CImage, CBox, CGrid, CButton } from '@chakra-ui/vue'
import { appSecret } from '../../secret'

export default {
  name: 'fetched-comp',
  data () {
    return {
      fetchedData: ''
    }
  },
  filters: {
    capitalize (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },
  mounted () {
    const baseUrl = 'https://dummyapi.io/data/api'
    axios.get(baseUrl + '/post', {
      headers: {
        'app-id': appSecret
      }
    })
      .then(data => { this.fetchedData = data.data })
  },
  components: {
    CFlex,
    CText,
    CImage,
    CBox,
    CGrid,
    CButton
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
