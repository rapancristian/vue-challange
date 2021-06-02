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

    <l-geo-json :geojson="geojson" v-if="geojson != null" ></l-geo-json>
    </l-map>
  </div>
</template>

<script>
import { latLng } from 'leaflet'
import { LMap, LTileLayer, LGeoJson } from 'vue2-leaflet'

export default {
  name: 'Map',
  props: {
    geojson: Object
  },
  components: {
    LMap,
    LTileLayer,
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
      mapOptions: {
        zoomSnap: 1
      }
    }
  },
  methods: {
    zoomUpdate (zoom) {
      this.currentZoom = zoom
    },
    centerUpdate (center) {
      this.currentCenter = center
    },
    showLongText () {
      this.showParagraph = !this.showParagraph
    }
  }
}
</script>
