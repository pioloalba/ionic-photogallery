<template>
  <ion-card class="camera-card">
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-button
        expand="block"
        :disabled="isTakingPicture"
        @click="takePicture"
      >
        <ion-spinner v-if="isTakingPicture" name="crescent" />
        <span v-else>Take Picture</span>
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p class="camera-error" role="alert">{{ errorMessage }}</p>
      </ion-text>

      <div v-if="capturedImage" class="preview-container">
        <ion-img
          :src="capturedImage"
          alt="Captured photo"
          class="captured-image"
        />
      </div>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  Camera,
  CameraResultType,
  CameraSource,
} from '@capacitor/camera';
import { Capacitor } from '@capacitor/core';
import {
  IonButton,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonImg,
  IonSpinner,
  IonText,
} from '@ionic/vue';
import { ref } from 'vue';

const capturedImage = ref<string | null>(null);
const errorMessage = ref('');
const isTakingPicture = ref(false);

const takePicture = async (): Promise<void> => {
  errorMessage.value = '';
  isTakingPicture.value = true;

  try {
    if (Capacitor.isNativePlatform()) {
      const permissionStatus = await Camera.requestPermissions({
        permissions: ['camera'],
      });

      if (permissionStatus.camera === 'denied') {
        throw new Error(
          'Camera access was denied. Please allow camera access and try again.',
        );
      }
    }

    const photo = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.Uri,
      source: CameraSource.Camera,
    });

    if (!photo.webPath) {
      throw new Error('The camera did not return an image.');
    }

    capturedImage.value = photo.webPath;
  } catch (error) {
    errorMessage.value =
      error instanceof Error
        ? error.message
        : 'Unable to access the camera. Please try again.';
  } finally {
    isTakingPicture.value = false;
  }
};
</script>

<style scoped>
.camera-card {
  margin: 0;
}

.camera-error {
  margin: 1rem 0 0;
}

.preview-container {
  margin-top: 1rem;
  overflow: hidden;
  border-radius: 0.5rem;
  background: var(--ion-color-light);
}

.captured-image {
  display: block;
  width: 100%;
  max-height: 28rem;
  object-fit: contain;
}

ion-spinner {
  margin-right: 0.5rem;
}
</style>
