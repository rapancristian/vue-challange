<template>
  <header>
    <h1>{{ title }}</h1>
  <Button
      v-show="homePage"
      @btn-click="$emit('load-markers')"
      text= "Load data"
      color= "Green"
    />

    <Button
      v-show="homePage"
    @btn-click="$emit('show-markers')"
      text= "Show data"
      color= "Green"
    />
    <div>
    <b-table striped hover :items="this.markers"></b-table>
    </div>
    <div><Map /></div>
  </header>
</template>

<script>
import Button from './Button'
import Map from './Map'
export default {
  name: 'Header',
  props: {
    title: String
  },
  components: {
    Map,
    Button
  },
  data () {
    return {
      markers: [],
      test: false
    }
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
