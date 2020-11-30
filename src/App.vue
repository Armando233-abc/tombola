<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  }
});
</script>

<style>

body{
  --verde: #59886b;
  --rosso: #c05555;
  --giallo: #ffc85c;
  --panna: #fff8c1;
  --bianco: #fff;
  
}
ion-content,ion-page{
  background-color: var(--verde) !important;
}
ion-tabs{
  background-color: var(--bianco) !important;
}
</style>