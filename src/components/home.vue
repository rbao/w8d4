<template>
  <div id="app">
    <h1>{{title}}</h1>

    <ul>
      <url-item v-for="url in urlDatabase" :url="url" :key="url.id" @edit="edit"></url-item>
    </ul>

    <form @submit.prevent="submit">
      <input v-model="urlObject.name" type="text" name="name">
      <input v-model="urlObject.longUrl" type="text" name="longUrl">
      <button type="submit">Submit</button>

      <button v-if="urlObject.id" @click="cancelEdit" type="button">Cancel</button>
    </form>
  </div>
</template>

<script>
import UrlItem from './url-item'

export default {
  name: 'Home',
  components: {
    UrlItem
  },
  data () {
    return {
      title: 'Tinyapp',
      urlObject: {
        id: 0,
        name: '',
        longUrl: ''
      },
      nextId: 3,
      urlDatabase: [
        {
          id: 1,
          name: 'Google',
          longUrl: 'http://google.ca'
        },
        {
          id: 2,
          name: 'Facebook',
          longUrl: 'http://facebook.ca'
        }
      ]
    }
  },
  mounted () {
    setTimeout(() => {
      this.title = 'TINYAPP'
    }, 3000)
  },
  computed: {
    newTitle () {
      return this.title + ' TEST'
    }
  },
  methods: {
    cancelEdit() {
      this.urlObject = {
        id: 0,
        name: '',
        longUrl: ''
      }
    },

    edit(url) {
      console.log('running parent event handler...')
      this.urlObject = Object.assign({}, url)
    },

    submit () {
      if (this.urlObject.id) {
        let targetUrl
        this.urlDatabase.forEach((url) => {
          if (this.urlObject.id === url.id) {
            targetUrl = url
          }
        })

        targetUrl.name = this.urlObject.name
        targetUrl.longUrl = this.urlObject.longUrl
      } else {
        this.urlObject.id = this.nextId
        this.nextId = this.nextId + 1

        this.urlDatabase.push(this.urlObject)
      }

      this.urlObject = {
        id: 0,
        name: '',
        longUrl: ''
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
