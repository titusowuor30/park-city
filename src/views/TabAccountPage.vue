<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
         <ion-title color="primary">Account Settimgs</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
           <ion-title size="large" color="primary">Account Settings</ion-title>
        </ion-toolbar>
      </ion-header>
      
      <account-settings/>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import AccountSettings from '@/components/AccountSettings.vue';



export default defineComponent({
  name: 'Tab3Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage,AccountSettings }
});
</script>