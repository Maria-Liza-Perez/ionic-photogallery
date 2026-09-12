<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Photo Gallery</ion-card-title>
      <ion-card-subtitle>Your selected photos</ion-card-subtitle>
    </ion-card-header>

    <ion-card-content>
      <ion-button expand="block" @click="selectPhotos">
        <ion-icon :icon="imagesOutline" slot="start"></ion-icon>
        Select Photos
      </ion-button>

      <div class="gallery">
        <div
          v-for="(photo, index) in photos"
          :key="index"
          class="gallery-item"
        >
          <img :src="photo" :alt="`Photo ${index + 1}`" />
        </div>
      </div>

      <p v-if="photos.length === 0" class="empty">
        No photos selected yet.
      </p>
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

import { imagesOutline } from 'ionicons/icons'
import {
  Camera,
  CameraResultType,
  CameraSource
} from '@capacitor/camera'

import { ref } from 'vue'

const photos = ref<string[]>([])

const selectPhotos = async () => {
  try {
    const result = await Camera.pickImages({
      quality: 90,
      limit: 10
    })

    for (const image of result.photos) {
      const photo = await Camera.getPhoto({
        quality: 90,
        resultType: CameraResultType.DataUrl,
        source: CameraSource.Photos
      })

      if (photo.dataUrl) {
        photos.value.push(photo.dataUrl)
      }
    }
  } catch (error) {
    console.log('Gallery error:', error)
  }
}
</script>

<style scoped>
.gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
  margin-top: 15px;
}

.gallery-item img {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 10px;
}

.empty {
  text-align: center;
  color: gray;
  margin-top: 20px;
}
</style>