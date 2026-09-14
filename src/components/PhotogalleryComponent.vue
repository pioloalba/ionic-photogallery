<template>
  <ion-card class="gallery-card">
    <ion-card-header>
      <ion-card-title>Photo Gallery</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      Your captured photos will appear here.
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
} from '@ionic/vue';
</script>

<style scoped>
.gallery-card {
  margin: 0;
}
</style>
