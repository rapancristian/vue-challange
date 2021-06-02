<template>
  <div>
    <h3>  <Button
      @btn-click="emitGeoJson"
      text= "Load data"
      color= "Green"
    /></h3>
    <md-table v-model="tableData" md-sort="name" md-sort-order="asc" md-card>
      <md-table-toolbar>
        <h1 class="md-title">Data</h1>
      </md-table-toolbar>

      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="Id" md-sort-by="Id" md-numeric>{{ item.Id }}</md-table-cell>
        <md-table-cell md-label="X" md-sort-by="X" md-numeric>{{ item.X }}</md-table-cell>
        <md-table-cell md-label="Y" md-sort-by="Y" md-numeric>{{ item.Y }}</md-table-cell>
        <md-table-cell md-label="AnnualAllowableCut" md-sort-by="AnnualAllowableCut" md-numeric>{{ item.AnnualAllowableCut }}</md-table-cell>
        <md-table-cell md-label="Species" md-sort-by="Species" md-numeric>{{ item.Species }}</md-table-cell>
        <md-table-cell md-label="DiameterBreastHeight" md-sort-by="DiameterBreastHeight" md-numeric>{{ item.DiameterBreastHeight }}</md-table-cell>
        <md-table-cell md-label="Quality" md-sort-by="Quality" md-numeric>{{ item.Quality }}</md-table-cell>
        <md-table-cell md-label="Parcel" md-sort-by="Parcel" md-numeric>{{ item.Parcel }}</md-table-cell>

      </md-table-row>
    </md-table>
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
      tableData: [{
        X: null,
        Y: null,
        Id: null,
        AnnualAllowableCut: null,
        Species: null,
        DiameterBreastHeight: null,
        Quality: null,
        Parcel: null
      }],
      jsonResponse: null
    }
  },
  methods: {
    async loadGeoJson () {
      const response = await fetch('response.json')
      this.jsonResponse = await response.json()
      this.$emit('load-geo-json-parent', this.jsonResponse)
    },
    emitGeoJson () {
      this.loadGeoJson().then(this.loadRows)
    },
    loadRows () {
      var row = []
      for (var i = 0; i < this.jsonResponse.features.length; i++) {
        var currentItem = {
          X: this.jsonResponse.features[i].geometry.coordinates[0],
          Y: this.jsonResponse.features[i].geometry.coordinates[1],
          Id: this.jsonResponse.features[i].properties.Id,
          AnnualAllowableCut: this.jsonResponse.features[i].properties.AnnualAllowableCut,
          Species: this.jsonResponse.features[i].properties.Species,
          DiameterBreastHeight: this.jsonResponse.features[i].properties.DiameterBreastHeight,
          Quality: this.jsonResponse.features[i].properties.Quality,
          Parcel: this.jsonResponse.features[i].properties.Parcel
        }
        row.push(currentItem)
      }
      this.tableData = row
    }
  }
}
</script>
