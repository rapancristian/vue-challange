<template>
  <header>
    <h1 class="txt-center text-info">{{ title }}</h1>
    <div> <Map :geojson="this.geojson" /> </div>
    <div> <Table @load-geo-json-parent="loadGeoJson" /></div>
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
  }
}
</script>
