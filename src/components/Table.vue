<template>
  <div>
  <Button
      @btn-click="emitGeoJson"
      text= "Load data"
      color= "Green"
    />
  <Button
      @btn-click="testRows"
      text= "Test Rows"
      color= "Blue"
    />
  </div>
</template>

<script>
import Button from './Button'
export default {
  name: 'Table',
  components: {
    Button
  },
  props: {
    geojson: Object
  },
  data () {
    return {
      jsonResponse: null,
      test: false
    }
  },
  methods: {
    async loadGeoJson () {
      const response = await fetch('response.json')
      this.jsonResponse = await response.json()
    },
    emitGeoJson () {
      this.loadGeoJson()
      this.$emit('load-geo-json-parent', this.jsonResponse)
    },
    testRows () {
      console.log('Hei')
      var row = []
      for (var i = 0; i < this.jsonResponse.features.length; i++) {
        console.log('Hei2 real')
        row.push(this.jsonResponse.features[i].geometry.coordinates[0])
        row.push(this.jsonResponse.features[i].geometry.coordinates[1])
        row.push(this.jsonResponse.features[i].properties.Id)
        console.log(this.jsonResponse.features[i].properties.Id)
        row.push(this.jsonResponse.features[i].properties.AnnualAllowableCut)
        console.log(this.jsonResponse.features[i].properties.AnnualAllowableCut)
        row.push(this.jsonResponse.features[i].properties.Species)
        console.log(this.jsonResponse.features[i].properties.Species)
        row.push(this.jsonResponse.features[i].properties.DiameterBreastHeight)
        console.log(this.jsonResponse.features[i].properties.DiameterBreastHeight)
        row.push(this.jsonResponse.features[i].properties.Quality)
        console.log(this.jsonResponse.features[i].properties.Quality)
        row.push(this.jsonResponse.features[i].properties.Parcel)
        console.log(this.jsonResponse.features[i].properties.Parcel)
      }
      console.log('Hei4 real')
      console.log(this.jsonResponse)
      console.log(row)
      return row
    }

  },
  computed: {
    tableRows: function () {
      var tableRows = []
      for (var i = 0; i < this.jsonResponse.features.length; i++) {
        tableRows.push(this.jsonResponse.features[i].geometry.coordinates[0])
        tableRows.push(this.jsonResponse.features[i].geometry.coordinates[1])
        tableRows.push(this.jsonResponse.features[i].properties.Id)
        tableRows.push(this.jsonResponse.features[i].properties.AnnualAllowableCut)
        tableRows.push(this.jsonResponse.features[i].properties.Species)
        tableRows.push(this.jsonResponse.features[i].properties.DiameterBreastHeight)
        tableRows.push(this.jsonResponse.features[i].properties.Quality)
        tableRows.push(this.jsonResponse.features[i].properties.Parcel)
      }
      return tableRows
    }
  }
}
</script>
