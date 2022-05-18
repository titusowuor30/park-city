<template>
  <ion-card>
    <ion-card-header>
      <ion-list>
        <ion-item lines="none">
          <ion-card-title color="primary">Book parking slot</ion-card-title>
          <!-- <ion-card-title color="danger" slot="end" @click="$emit('close-modal',/ 1)">X</ion-card-title> -->
        </ion-item>
      </ion-list>
    </ion-card-header>
  </ion-card>
  <ion-card> </ion-card>

  <ion-card>
    <ion-card-header>
      <ion-card-title color="primary"></ion-card-title>
      <ion-card-subtitle></ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <ion-text mode="ios" class="booking-style">
        <h2>Parking Slot Name</h2>
        <h1>Sample Parking Slot</h1>
      </ion-text>
      <ion-card-content></ion-card-content>
      <ion-text mode="ios" class="booking-style">
        <h2>DateTime</h2>
        <h1>Wednesday, 21st April 2022</h1>
      </ion-text>
    </ion-card-content>
  </ion-card>

  <ion-card>
    <ion-card-header>
      <ion-item lines="none">
        <ion-card-title color="primary">M-Pesa</ion-card-title>
        <ion-button fill="solid" slot="end">KES {{ amount }}</ion-button>
      </ion-item>
    </ion-card-header>

    <ion-card-content>
      <ion-item>
        <ion-label position="floating">Total hours</ion-label>
        <ion-input
          type="number"
          v-model="hours"
          @change="calculateParkingFee()"
        ></ion-input>
      </ion-item>
      <ion-item>
        <ion-label position="floating" v-model="phone"
          >Enter phone number</ion-label
        >
        <ion-input type="number"></ion-input>
      </ion-item>
    </ion-card-content>
    <ion-button expand="block" @click="makePayments()">Pay Now</ion-button>
    <ion-loading
      :is-open="isOpenRef"
      cssClass="my-custom-class"
      message="Please wait..."
      :duration="timeout"
      @didDismiss="setOpen(false)"
    >
    </ion-loading>
  </ion-card>
</template>

<script>
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonItem,
  IonLabel,
  IonInput,
  IonButton,
  IonIcon,
  IonLoading,
} from "@ionic/vue";
import { pin, walk, warning, wifi, wine } from "ionicons/icons";
import { defineComponent, ref } from "vue";
import axios from "axios";

export default defineComponent({
  props: {
    timeout: { type: Number, default: 3000 },
  },
  components: {
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardSubtitle,
    IonCardTitle,
    IonButton,
    IonItem,
    IonLabel,
    IonInput,
    IonLoading,
    // IonIcon,
  },
  data() {
    return {
      hours: 1,
      phone: "",
      amount: 10,
      info:[],
      paymentstatus:"",
    };
  },
  mounted() {
    this.calculateParkingFee();
  },
  methods: {
    calculateParkingFee() {
      this.amount = Number(this.hours) * this.amount;
    },
    makePayments() {
      this.setOpen(true);
      axios
        .post("https://5d47-154-159-237-52.in.ngrok.ioo/citypark/online/lipa")
        .then((response) => (console.log("data 1")))
        .then(() => {
          axios
            .post("https://5d47-154-159-237-52.in.ngrok.io/citypark/callback/")
            .then((res) => {
              if (res.data) {
                console.log(res.data);
                this.paymentstatus = "Success";
                this.$route.push({ path: "/bookings" });
              } else {
                this.paymentstatus = "Failed";
              }
            });
        })
        .catch((error) => console.log(error));
    },
  },
  setup() {
    const isOpenRef = ref(false);
    const setOpen = (state) => (isOpenRef.value = state);
    return { warning, isOpenRef, setOpen };
  },
});
</script>

<style scoped>
.booking-style {
  padding-top: 17px !important;
}
</style>