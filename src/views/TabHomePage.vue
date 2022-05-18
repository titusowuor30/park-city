<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title color="primary">Find a parking slot</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large" color="primary"
            >Find a parking slot</ion-title
          >
        </ion-toolbar>
      </ion-header>
      <map-container/>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import MapContainer from "@/components/MapContainer.vue";

export default defineComponent({
  name: "Tab1Page",
  components: {
    MapContainer,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
  },
});
</script>
