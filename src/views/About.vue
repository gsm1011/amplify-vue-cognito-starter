<template>
  <div>
    <h1>This is server information.</h1>
    <h3>
      {{ info }}
    </h3>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      info: ''
    }
  },
  mounted () {
    const url = 'https://8ij2y4wpr9.execute-api.us-east-1.amazonaws.com/dev/m'
    if (this.$store.state.user) {
      const jwt = this.$store.state.user
                  .getSignInUserSession()
                  .getIdToken()
                  .getJwtToken()
      const config = {
        headers: {
          Authorization: jwt
        }
      }
      axios.get(url, config)
      .then(val => {
        console.log(val)
        this.info = val
      })
      .catch(e => console.log(e))
    }
  }
}
</script>