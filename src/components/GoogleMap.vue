<template>
  <div class="map" ref="mapDivRef"></div>
</template>

<script>
import { ref, onBeforeMount, onMounted, watch } from "vue";

export default {
  name: "GoogleMap",
  props: {
    center: { lat: Number, lng: Number },
    zoom: Number,
    mapType: String,
    disableUI: Boolean,
    markers: Array,
  },
  setup(props) {
    // the google map object
    const map = ref(null);

    // the map element in the templste
    const mapDivRef = ref(null);

    // load in the google script
    onBeforeMount(() => {
      // key is is the .env file
      //   const key = process.env.VUE_APP_GOOGLEMAPS_KEY;

      const key = "AIzaSyAIH4XrdSkwiQlakBvmQMyKtqhwvLyeHeQ";

      //   console.log(key)

      // create the script element to load
      const googleMapScript = document.createElement("SCRIPT");
      googleMapScript.setAttribute(
        "src",
        `https://maps.googleapis.com/maps/api/js?key=${key}&callback=initMap`
      );
      googleMapScript.setAttribute("defer", "");
      googleMapScript.setAttribute("async", "");
      document.head.appendChild(googleMapScript);
    });

    const loadMarkers = () => {
      const mapIcon = "../../assets/map.png";
      if (!props.markers.length) return;

      props.markers.forEach((markerInfo) => {
        const mapMarker = new window.google.maps.Marker({
          position: new window.google.maps.LatLng(
            markerInfo.lat,
            markerInfo.lng
          ),
          map: map.value,
          title: markerInfo.title,
          icon: mapIcon,
        });

        mapMarker.infoWindow = new window.google.maps.InfoWindow({
          content: `<strong> ${markerInfo.title} </strong>`,
        });

        mapMarker.addListener("click", () => {
          if (mapMarker.infoWindow !== null) {
            mapMarker.infoWindow.open(map.value, mapMarker);
          }
        });
      });
    };

    const setTrafficLayer = () => {
      const trafficLayer = new window.google.maps.TrafficLayer();
      trafficLayer.setMap(map.value);
    };

    const addMarker = (lat, lng) => {
        const userIcon = "../../assets/car.png"
      new window.google.maps.Marker({
        position: { lat, lng },
        map: map.value,
        icon: userIcon
      });
    };

    watch(
      () => props.markers,
      () => {
        loadMarkers();
      }
    );

    /**
     * this function is called as soon as the map is initialized
     */
    window.initMap = () => {
      map.value = new window.google.maps.Map(mapDivRef.value, {
        mapTypeId: props.mapType || "hybrid",
        zoom: props.zoom || 8,
        disableDefaultUI: props.disableUI || true,
        center: { lat: -1.29, lng: 36.82 },
      });

      addMarker(-1.3, 36.86);
      loadMarkers();
      setTrafficLayer();
    };

    return {
      mapDivRef,
    };
  },
};
</script>

<style lang="css" scoped>
.map {
  width: 100%;
  height: 50%;
  background-color: azure;
}
</style>