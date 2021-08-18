<template>
  <q-page style="display: flex; flex-direction: column">
    <div style="position: relative; flex: 1 1 50%">
      <div
        id="map"
        ref="map"
        style="position: absolute; top: 0; bottom: 0; left: 0; right: 0"
      >
        <img
          src="~assets/pin.svg"
          style="
            position: absolute;
            width: 36px;
            margin-left: -18px;
            bottom: 50%;
            left: 50%;
            z-index: 999;
          "
        />
      </div>
    </div>
    <div style="flex: 1 0 0; overflow-y: auto">
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
      <q-input outlined label="Standout" />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, onMounted, reactive } from "vue";

export default defineComponent({
  name: "PageIndex",
  setup() {
    const data = reactive({});
    onMounted(() => {
      console.log("onMounted");

      ymaps.ready(async () => {
        console.log("ymaps ready");
        let position = {};

        try {
          position = await this.getCurrentPosition();
        } catch (err) {
          position = {
            latitude: 55.75399399999374,
            longitude: 37.62209300000001,
          };
        }

        this.myMap = new ymaps.Map("map", {
          center: [position.latitude, position.longitude],
          // Уровень масштабирования. Допустимые значения:
          // от 0 (весь мир) до 19.
          zoom: 15,
          controls: ["typeSelector", "geolocationControl", "searchControl"],
        });
      });
    });

    return { data };
  },
});
</script>
