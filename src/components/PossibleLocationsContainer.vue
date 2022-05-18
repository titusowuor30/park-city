<template>
  <ion-list class="possible-locations-class">
    <ion-list-header lines="inset" v-for="marker in markers" :key="marker">
      <ion-label class="possible-locations-class" @click="showBookingModal">{{
        marker.title
      }}</ion-label>
      <ion-button>{{
        getDistance(-1.3, 36.86, marker.lat, marker.lng)
      }}</ion-button>
    </ion-list-header>
  </ion-list>

</template>

<script>
import { IonLabel, IonList, IonListHeader } from "@ionic/vue";

import { computed, defineComponent } from "vue";


export default defineComponent({
  components: {
    IonLabel,
    IonList,
    IonListHeader,
 
  },
  props: {
    markers: Array,
  },
  data() {
   return{
        modalEnabled: false
   }
  },
  setup() {
    return {
      enableBackdropDismiss: true,
      showBackdrop: false,
      shouldPropagate: true,
    };
  },
  methods: {
    getDistance(lat1, lng1, lat2, lng2) {
      let rad = (x) => (x * Math.PI) / 180;

      let R = 6378137; // Earth’s mean radius in meter
      let dLat = rad(lat2 - lat1);
      let dLong = rad(lng2 - lng1);
      let a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(rad(lat1)) *
          Math.cos(rad(lat2)) *
          Math.sin(dLong / 2) *
          Math.sin(dLong / 2);
      let c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
      let d = R * c;
      return `${(d / 1000).toFixed(2)} ${"km"}`; // returns the distance in km
    },

    showBookingModal() {
      this.modalEnabled = !this.modalEnabled;
       this.$emit('modal-visilibity', this.modalEnabled)
    },
  },
});
</script>
<style scoped>
.possible-locations-class {
  font-size: 17px;
  font-weight: 500;
}
</style>