<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
      <ion-card-subtitle>Take a photo</ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <div v-if="photo" class="photo-container">
        <img :src="photo" alt="Captured Photo" />
      </div>

      <ion-button expand="block" @click="takePhoto">
        <ion-icon :icon="cameraOutline" slot="start"></ion-icon>
        Take Photo
      </ion-button>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardContent,
  IonButton,
  IonIcon
} from '@ionic/vue'

import { cameraOutline } from 'ionicons/icons'
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera'
import { ref } from 'vue'

const photo = ref<string | undefined>()

const takePhoto = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    })

    photo.value = image.dataUrl
  } catch (error) {
    console.log('Camera error:', error)
  }
}
</script>

<style scoped>
.photo-container {
  width: 100%;
  margin-bottom: 15px;
}

.photo-container img {
  width: 100%;
  max-height: 400px;
  object-fit: cover;
  border-radius: 12px;
}
</style>