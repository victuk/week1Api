<template>
  <div class="fetched-comp">
  <router-link to="/post">
  <CBox>
        <CButton>
            View Posts
        </CButton>
    </CBox>
    </router-link>
  <div v-for="people in fetchedData.data" :key="people.id">
  <c-grid w="100%" template-columns="repeat(2, 1fr)" gap="6">
  <c-stack :spacing="5">
    <c-box :p="5" shadow="md" border-width="1px">
    <img :src="people.picture" style="width: 100px; width: 100px; border-radius:50%" /> <br />
        <c-heading>{{people.title | capitalize}} {{people.lastName}}, {{people.firstname}}</c-heading><br />
        <c-text :mt="4">Email: {{people.email}}</c-text><br />
        <router-link :to="'/user/' + people.id">
        <c-button variant-color="blue" variant="outline">
        View Profile
        </c-button>
        </router-link>
    </c-box>
</c-stack>
</c-grid>
  </div>
  </div>
</template>

<script>

import { CBox, CButton, CStack, CGrid } from '@chakra-ui/vue'
import axios from 'axios'
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
    axios.get(baseUrl + '/user', {
      headers: {
        'app-id': appSecret
      }
    })
      .then(data => { this.fetchedData = data.data })
  },
  methods: {
    viewProfile (profileID) {
      console.log(profileID)
    }
  },
  components: {
    CBox,
    CButton,
    CStack,
    CGrid
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
