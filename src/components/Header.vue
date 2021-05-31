<template>
  <header>
    <h1>{{ title }}</h1>
  <Button
      v-show="homePage"
      @btn-click="$emit('load-markers')"
      text= "Load data"
      color= "Green"
    />
  </header>
</template>

<script>
import Button from './Button'

export default {
  name: 'Header',
  props: {
    title: String
  },
  components: {
    Button
  },
  computed: {
    homePage () {
      if (this.$route.path === '/') {
        return true
      } else {
        return false
      }
    }
  }
}
</script>
