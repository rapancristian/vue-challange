<template>
  <div>
  <Button
      @btn-click="emitGeoJson"
      text= "Load data"
      color= "Green"
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
    }
  }
}
</script>
