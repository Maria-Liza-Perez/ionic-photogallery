<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Photo App</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">

      <div class="welcome">
        <h1>Welcome!</h1>
        <p>Take and manage your photos.</p>
      </div>

      <CameraComponents />

      <PhotoGalleryComponents />

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent
} from '@ionic/vue'

import CameraComponents from '@/components/CameraComponents.vue'
import PhotoGalleryComponents from '@/components/PhotoGalleryComponents.vue'
</script>

<style scoped>
.welcome {
  text-align: center;
  margin-bottom: 20px;
}

.welcome h1 {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 5px;
}

.welcome p {
  color: gray;
}
</style>