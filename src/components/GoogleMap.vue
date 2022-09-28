<template>
  <div>
    <h1 style="text-align: center">Google Maps</h1>

    <nav class="nav">
      <select name="" id="" v-model="fromLocation">
        <option value="">--from--</option>
        <option
          v-for="(eachLocation, index) in locations"
          v-bind:key="index"
          v-bind:value="eachLocation.loc"
        >
          {{ eachLocation.name }}
        </option>
      </select>

      <select name="" id="" v-model="toLocation">
        <option value="">--to--</option>
        <option
          v-for="(eachLocation, index) in locations"
          v-bind:key="index"
          v-bind:value="eachLocation.loc"
        >
          {{ eachLocation.name }}
        </option>
      </select>

      <button v-on:click="calculateRoute(fromLocation, toLocation)">
        Get Route!
      </button>

      <button v-on:click="clearRoutes()">Clear!</button>
    </nav>

    <div id="map"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      map: null,
      directionsDisplay: null,
      service: null,
      locations: [
        { name: "balboaPark", loc: { lat: 32.7341, lng: -117.1446 } },
        { name: "petcoPark", loc: { lat: 32.7075, lng: -117.1575 } },
        { name: "sanDiegoAirport", loc: { lat: 32.7323, lng: -117.196 } },
      ],
      fromLocation: "",
      toLocation: "",
    };
  },
  methods: {
    /*
     * Initialize map
     * https://developers.google.com/maps/documentation/javascript/overview
     */
    initMap() {
      const mapElement = document.getElementById("map");
      const mapOptions = {
        center: this.locations[0].loc,
        zoom: 13,
        mapTypeId: window.google.maps.MapTypeId.ROADMAP,
        panControl: true,
        zoomControl: true,
        mapTypeControl: true,
        scaleControl: true,
        streetViewControl: true,
        overviewMapControl: true,
        rotateControl: true,
      };

      this.map = new window.google.maps.Map(mapElement, mapOptions);
      this.addMarker();
    },
    /*
     * Add Marker
     */
    addMarker() {
      const marker = new window.google.maps.Marker({
        position: this.locations[0].loc,
        animation: window.google.maps.Animation.DROP,
        draggable: true,
      });
      marker.setMap(this.map);
    },
    /*
     * Calculate route between 2 Coordinates
     * https://stackoverflow.com/questions/27341214/how-to-draw-a-route-between-two-markers-in-google-maps
     * input start: { lat: 32.7341, lng: -117.1446 }
     * input end: { lat: 32.7075, lng: -117.1575 }
     */
    calculateRoute(start, end) {
      const request = {
        origin: start,
        destination: end,
        // https://developers.google.com/maps/documentation/transportation-logistics/on-demand-rides-deliveries-solution/pickup-and-dropoff-selection/location-selection/reference/rest/v1beta/TravelMode
        travelMode: window.google.maps.TravelMode.TWO_WHEELER,
      };

      this.directionsDisplay.setMap(this.map);

      this.service.route(request, (response, status) => {
        if (status == window.google.maps.DirectionsStatus.OK) {
          this.directionsDisplay.setDirections(response);
          this.directionsDisplay.setMap(this.map);
        } else {
          alert(
            "Directions Request from " +
              start.toUrlValue(6) +
              " to " +
              end.toUrlValue(6) +
              " failed: " +
              status
          );
        }
      });
    },
    clearRoutes() {
      this.directionsDisplay.setMap(null);
    },
  },
  mounted() {
    // Initialize map after DOM is mounted
    this.initMap();
    this.directionsDisplay = new window.google.maps.DirectionsRenderer();
    this.service = new window.google.maps.DirectionsService();
  },
};
</script>

<style scoped>
#map {
  grid-area: map;
  width: 500px;
  height: 400px;
  padding: 25px;
  margin: 25px auto;
}
.nav {
  text-align: center;
}
</style>