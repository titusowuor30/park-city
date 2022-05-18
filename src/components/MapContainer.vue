<template>
  <google-map
    :disableUI="true"
    :zoom="12"
    mapType="roadmap"
    :center="{ lat: 38.8977859, lng: -77.0057621 }"
    :markers="markers"
  >
  </google-map>
  <ion-card>
    <ion-card-header>
      <ion-card-title id="self-help" color="primary"
        >NEAREST PARKING LOTS</ion-card-title
      >
    </ion-card-header>
    <ion-card-content>
      <possible-locations-container
        :markers="markers"
        @modal-visilibity="modalVisilibity"
      />
      <location-confirm-container-vue v-if="modalEnabled" />
    </ion-card-content>
  </ion-card>
  
</template>

<script>
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
} from "@ionic/vue";
import { warning } from "ionicons/icons";
import PossibleLocationsContainer from "@/components/PossibleLocationsContainer.vue";
import GoogleMap from "@/components/GoogleMap.vue";
import LocationConfirmContainerVue from "./LocationConfirmContainer.vue";

import { defineComponent, reactive, getCurrentInstance } from "vue";
// import axios from "axios";

export default defineComponent({
  components: {
    PossibleLocationsContainer,
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardTitle,
    GoogleMap,
    LocationConfirmContainerVue,
  },
  data() {
    return {
      modalEnabled: false,
    };
  },
  setup() {
    const markers = reactive([
      {
        lat: -1.3081605991149625,
        lng: 36.84961328697481,
        title: "Hazina Complex Parking lor",
        icon: "../../assets/map.png",
      },
      {
        lat: -1.3050714978182774,
        lng: 36.824550727029106,
        title: "Parking Lot B",
        icon: "../../assets/map.png",
      },
      {
        lat: -1.2913421129405398,
        lng: 36.806011299124066,
        title: "Kenyatta parking lot",
        icon: "../../assets/map.png",
      },
      {
        lat: -1.289282698793264,
        lng: 36.80120478077832,
        title: "Melody",
        icon: "../../assets/map.png",
      },
      {
        lat: -1.2700614201053557,
        lng: 36.80875788103593,
        title: "Ufungamano Parking",
        icon: "../../assets/map.png",
      },
    ]);

    return { warning, markers };
  },
  methods: {
    modalVisilibity(visible) {
      this.modalEnabled = visible;
    },
  },
});
</script>

<style scoped>
#self-help {
  padding-left: 20px;
  font-size: 15px;
}
</style>