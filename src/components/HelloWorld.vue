<template>
  <div class="hello">
    <div v-if="signedIn">
      <amplify-sign-out></amplify-sign-out>
    </div>
    <div v-else>
      <amplify-authenticator></amplify-authenticator>
    </div>
  </div>
</template>

<script>
import { components, AmplifyEventBus } from 'aws-amplify-vue'
import { Auth } from 'aws-amplify'

export default {
  name: 'HelloWorld',
  components: {
    ...components
  },
  props: {
    msg: String
  },
  created () {
    const store = this.$store
    this.findUser(store)
    AmplifyEventBus.$on("authState", (info) => {
      if (info === 'signedIn') {
        this.findUser(store)
      } else {
        store.state.signedIn = false
        store.state.user = null
      }
    })
  },
  computed: {
    signedIn () {
      return this.$store.state.signedIn
    }
  },
  methods: {
    async findUser (store) {
      try {
        const user = await Auth.currentAuthenticatedUser()
        // this.signedIn = true
        store.state.signedIn = true
        store.state.user = user
        // console.log(user)
      } catch (e) {
        // console.log(e)
        store.state.signedIn = false
        store.state.user = null
      }
    }
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
