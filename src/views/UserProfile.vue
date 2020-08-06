<template>
    <div class="home">
    <HelloWorld :msg="'Welcome ' + fetchedData.firstName + ' to your Profile'"/>
        <img :src="fetchedData.picture" style="width: 100px; width: 100px; border-radius:50%" /> <br />
    <c-list spacing="3">
    <c-list-item>
    <c-icon name="star" color="green.500" />
    Title:{{fetchedData.title | capitalize}}<br />
    Surname:{{fetchedData.lastName}}<br />
    First Name{{fetchedData.firstname}}
  </c-list-item>
  <c-list-item>
  <c-icon name="email" color="green.500" />
    Email: {{fetchedData.email}}
        Street: {{fetchedData.location.street}}
        City: {{fetchedData.location.city}}
        State: {{fetchedData.location.state}}
        Country: {{fetchedData.location.country}}
        Time Zone: {{fetchedData.location.timezone}}
  </c-list-item>
</c-list>
<c-button variant-color="blue">View your Posts</c-button>
  </div>
</template>
<script>
// <router-link :to="'/user/' + people.id"> the link </router-link>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { CList, CListItem, CIcon, CButton } from '@chakra-ui/vue'
import axios from 'axios'
import { appSecret } from '../../secret'

export default {
  name: 'Home',
  data () {
    return {
      fetchedData: ''
    }
  },
  mounted () {
    const baseUrl = 'https://dummyapi.io/data/api'
    axios.get(baseUrl + '/user/' + this.$route.params.id, {
      headers: {
        'app-id': appSecret
      }
    })
      .then(data => { this.fetchedData = data.data })
  },
  filters: {
    capitalize (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },
  components: {
    HelloWorld,
    CList,
    CListItem,
    CIcon,
    CButton
  }
}
</script>
