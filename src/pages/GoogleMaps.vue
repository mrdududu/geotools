<template>
  <q-page style="display: flex; flex-direction: column">
    <div>Google Map</div>
    <div>latitude: {{ currPos.lat }}</div>
    <div>longitude: {{ currPos.lng }}</div>
    <div ref="mapDiv" style="width: 100%; height: 80vh" />
  </q-page>
</template>
<script>
/* eslint-disable no-undef */
import { defineComponent, computed, onMounted, ref } from "vue";
import { useGeolocation } from "../functions/useGeolocation";
import { Loader } from "@googlemaps/js-api-loader";

const GOOGLE_MAPS_API_KEY = "AIzaSyCj0jKcxDq6YlovBf5_VlHMmILYiXruu7o";

export default defineComponent({
  setup() {
    const { coords } = useGeolocation();
    const currPos = computed(() => ({
      lat: coords.value.latitude,
      lng: coords.value.longitude,
    }));

    const loader = new Loader({ apiKey: GOOGLE_MAPS_API_KEY });
    const mapDiv = ref(null);
    let map = ref(null);

    onMounted(async () => {
      await loader.load();
      map.value = new google.maps.Map(mapDiv.value, {
        center: currPos.value,
        zoom: 7,
      });

      map.value.addListener("center_changed", () => {
        const center = map.value.getCenter();
        console.log("center_changed", center, center.lat(), center.lng());
      });
    });

    return { currPos, mapDiv };
  },
});
</script>
