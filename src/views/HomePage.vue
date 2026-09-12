<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <CameraComponent @photo-captured="addPhoto" />

      <PhotoGalleryComponent :photos="photos" />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";

import { ref } from "vue";

import CameraComponent from "../components/CameraComponents.vue";
import PhotoGalleryComponent from "../components/PhotoGalleryComponents.vue";

const photos = ref<string[]>([]);

// Add captured photo to gallery
const addPhoto = (photo: string) => {
  photos.value.unshift(photo);

  console.log("Photo added to gallery!");
};
</script>