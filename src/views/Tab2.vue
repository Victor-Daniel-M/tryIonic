<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Photo Gallery</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid>
        <ion-row> {{ deviceInfoJson }} </ion-row>
        <ion-row>
          <ion-col size="6" :key="photo" v-for="photo in photos">
            <ion-img :src="photo.webviewPath" @click="logDeviceInfo"></ion-img>
          </ion-col>
        </ion-row>
      </ion-grid>
      <ion-fab vertical="bottom" horizontal="center" slot="fixed">
        <ion-fab-button @click="takePhoto()">
          <ion-icon :icon="camera"></ion-icon>
        </ion-fab-button>
      </ion-fab>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { usePhotoGallery, UserPhoto } from "@/composables/usePhotoGallery";
import { camera, trash, close } from "ionicons/icons";
import { Device } from "@capacitor/device";
import {
  IonPage,
  IonHeader,
  IonFab,
  IonFabButton,
  IonIcon,
  IonToolbar,
  IonTitle,
  IonContent,
  IonGrid,
  IonRow,
  IonCol,
  IonImg,
} from "@ionic/vue";
import { ref } from "@vue/reactivity";

export default {
  name: "Tab2",
  components: {
    IonPage,
    IonHeader,
    IonFab,
    IonFabButton,
    IonIcon,
    IonToolbar,
    IonTitle,
    IonContent,
  },
  setup() {
    const { photos, takePhoto } = usePhotoGallery();
    const deviceInfoJson = ref("");

    function log() {
      console.log("Logging2");
    }

    const logDeviceInfo = async () => {
      const info = await Device.getId();

      deviceInfoJson.value = JSON.stringify(info);
    };

    return {
      photos,
      takePhoto,
      logDeviceInfo,
      deviceInfoJson,
      camera,
      trash,
      close,
    };
  },
};
</script>