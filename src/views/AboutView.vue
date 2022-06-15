<template>
  <div class="about">
    <h1>This is a map page</h1>
    <div id="map"></div>
  </div>
</template>

<script>
/* global mapboxgl */
export default {
  data: function () {
    return {
      places: [
        { lat: -25.363, lng: 131.044, description: "A place in Australia" },
        { lat: -33.8675, lng: 151.207, description: "The main city!" },
        { lat: 39.1911, lng: -106.8175, description: "The Motherland" },
        { lat: 45.0319, lng: -110.7058, description: "Might be underwater..." },
        { lat: 20.868, lng: -105.44, description: "I'd get married here..." },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MY_API_KEY;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/outdoors-v11", // style URL
      center: [-112.2097, 47.3297], // starting position [lng, lat]
      zoom: 6, // starting zoom
    });

    const marker1 = new mapboxgl.Marker().setLngLat([-111.0429, 45.677]).addTo(map);
    const popup = new mapboxgl.Popup({ closeOnClick: false })
      .setLngLat([-112.2097, 47.3297])
      .setHTML("<h1>Last Best Ski Country</h1>")
      .addTo(map);

    this.places.forEach((place) => {
      new mapboxgl.Marker().setLngLat([place.lng, place.lat]).addTo(map);
      new mapboxgl.Popup({ closeOnClick: false })
        .setLngLat([place.lng, place.lat])
        .setHTML("<small>" + place.description + "</small>")
        .addTo(map);
    });
    console.log(map, popup, marker1);
  },
};
</script>
<style>
body {
  margin: 0;
  padding: 0;
}
#map {
  position: absolute;
  top: 100;
  bottom: 100;
  width: 1000px;
  height: 600px;
}
</style>
