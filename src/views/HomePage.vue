<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Photo Gallery</ion-title>
        </ion-toolbar>
      </ion-header>

      <div class="gallery-layout">
        <section class="gallery-section">
          <CameraComponent />
        </section>
        <section class="gallery-section">
          <PhotogalleryComponent />
        </section>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
} from '@ionic/vue';
import CameraComponent from '../components/CameraComponent.vue';
import PhotogalleryComponent from '../components/PhotogalleryComponent.vue';
</script>

<style scoped>
.gallery-layout {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 72rem;
  margin: 0 auto;
  padding: 1rem;
  box-sizing: border-box;
}

.gallery-section {
  width: 100%;
}

@media (min-width: 768px) {
  .gallery-layout {
    padding: 1.5rem;
  }
}
</style>
