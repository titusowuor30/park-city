<template>
  <!-- Default -->
  <ion-modal
    :is-open="true"
    mode="ios"
    show-backdrop="true"
    swipe-to-close="true"
  >
    <ion-content class="container-top">
      <booking-card />
    </ion-content>
  </ion-modal>
</template>

<script>
import { IonModal, IonContent } from "@ionic/vue";
import { defineComponent } from "vue";
import BookingCard from "./BookingCard.vue";

export default defineComponent({
  components: { IonModal, IonContent, BookingCard },
});
</script>

<style scoped>
.container-top {
  padding: 20px;
}
</style>