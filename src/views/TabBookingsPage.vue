

<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title color="primary">My Bookings</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large" color="primary">My Bookings</ion-title>
        </ion-toolbar>
      </ion-header>
      
      <booking-list/>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import BookingList from '@/components/BookingList.vue';


export default defineComponent({
  name: 'Tab2Page',
  components: {  IonHeader, IonToolbar, IonTitle, IonContent, IonPage,BookingList }
});
</script>
