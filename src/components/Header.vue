<template>
  <header>
    <h1>{{ title }}</h1>
    <div>
      <Button
      @btn-click="testButton"
      text= "Test Button"
      color= "Red"
    />
    </div>
    <div> <Table @load-geo-json-parent="loadGeoJsonParent" /></div>
    <div> <Map :geojson="this.geojson" /> </div>
  </header>
</template>

<script>
import Button from './Button'
import Table from './Table'
import Map from './Map'

export default {
  name: 'Header',
  props: {
    title: String
  },
  components: {
    Map,
    Table,
    Button
  },
  data () {
    return {
      geojson: null,
      test: false
    }
  },
  methods: {
    testButton () {
      console.log(this.geojson.features[0].properties)
    },
    loadGeoJsonParent (value) {
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
