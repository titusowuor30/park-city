<template>
  <!-- List of Input Items -->
  <ion-list>
    <ion-item>
      <ion-label color="medium">Notifications</ion-label>
    </ion-item>
    <ion-item>
      <ion-label>Enable Email Notifications</ion-label>
      <ion-toggle slot="end"></ion-toggle>
    </ion-item>
    <ion-item>
      <ion-label>Enable Push Notifications</ion-label>
      <ion-toggle slot="end"></ion-toggle>
    </ion-item>
    <ion-item>
      <ion-label></ion-label>
      <ion-radio slot="end"></ion-radio>
    </ion-item>
    <ion-item>
      <ion-label color="medium">General Settings</ion-label>
    </ion-item>
    <ion-item>
      <ion-label>Subscribe to mailing list</ion-label>
      <ion-checkbox slot="start"></ion-checkbox>
    </ion-item>
    <ion-item>
      <ion-label>Enable faster checkout</ion-label>
      <ion-checkbox slot="start"></ion-checkbox>
    </ion-item>
  </ion-list>
</template>

<script>
import {
  IonCheckbox,
  IonItem,
  IonList,
  IonLabel,
  IonRadio,
  IonToggle,
} from "@ionic/vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    IonCheckbox,
    IonItem,

    IonList,
    IonLabel,
    IonRadio,
    IonToggle,
  },
});
</script>