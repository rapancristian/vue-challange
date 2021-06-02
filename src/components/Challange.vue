<template>
  <header>
    <h1>{{ title }}</h1>
    <div> <Table @load-geo-json-parent="loadGeoJson" /></div>
    <div> <Map :geojson="this.geojson" /> </div>
  </header>
</template>

<script>
import Table from './Table'
import Map from './Map'

export default {
  name: 'Challange',
  props: {
    title: String
  },
  components: {
    Map,
    Table
  },
  data () {
    return {
      geojson: null
    }
  },
  methods: {
    loadGeoJson (value) {
      this.geojson = value
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
