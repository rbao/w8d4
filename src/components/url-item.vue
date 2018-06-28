<template>
  <li>
    <span>{{url.name}}</span> - <a :href="url.longUrl">{{url.longUrl}}</a>
    <button @click="onEdit" type="button">Edit</button>
  </li>
</template>

<script>
export default {
  name: 'UrlItem',
  props: {
    url: {
      type: Object,
      required: true
    }
  },
  methods: {
    onEdit() {
      console.log('running child event handler...')
      this.$emit('edit', this.url)
    }
  }
}
</script>

<style scoped>
button {
  font-size: 24px;
}
</style>
