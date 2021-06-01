 <template>
 <div style="height: 500px; width: 100%">
    <div style="height: 200px; overflow: auto;">
    </div>
    <l-map
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 80%"
      @update:center="centerUpdate"
      @update:zoom="zoomUpdate"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />

     <l-marker v-for="item in markers" :key="item.id" :lat-lng="item.latlng" @add="onAdd($event)">
    </l-marker>
    <l-geo-json :geojson="geojson"></l-geo-json>
    </l-map>
  </div>
</template>

<script>
import { latLng } from 'leaflet'
import { LMap, LTileLayer, LMarker, LGeoJson } from 'vue2-leaflet'

export default {
  name: 'Map',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LGeoJson
  },
  data () {
    return {
      zoom: 3,
      center: latLng(25.97363, 27.29368),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      currentZoom: 11.5,
      currentCenter: latLng(25.97363, 27.29368),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 1
      },
      markers: [],
      geojson: null
    }
  },
  mounted () {
    window.setTimeout(this.addMarker, 2000)
  },
  methods: {
    addMarker () {
      this.markers.push({
        id: 1,
        latlng: latLng(47.413220, -1.219483),
        content: 'Hi! this is my popup data'
      })
    },
    onAdd: function (e) {
      this.$nextTick(() => e.target.openPopup())
    },
    zoomUpdate (zoom) {
      this.currentZoom = zoom
    },
    centerUpdate (center) {
      this.currentCenter = center
    },
    showLongText () {
      this.showParagraph = !this.showParagraph
    },
    innerClick () {
      alert('Click!')
    }
  },
  async created () {
    const response = await fetch('response.json')
    this.geojson = await response.json()
  }
}
</script>
