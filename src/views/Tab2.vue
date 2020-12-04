<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Numeri estratti</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-searchbar placeholder="Cerca numero" @input="filtra($event)"></ion-searchbar>
      
      <ul class="estratti">
          <li class="estratto" v-for="(numero, i) in listaEstratti" :key="i">{{numero}}</li>
      </ul>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';

export default  {
  name: 'Tab2',
  components: {  IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  mounted(){
    const leggiDati = ()=> {
      const listaEstrattiStr = localStorage.getItem("estratti")
      const listaEstratti = JSON.parse(listaEstrattiStr) 
      this.listaEstratti = listaEstratti.filter(numero=>numero.toString().includes(this.numeroDaCercare))
    }
    setInterval(leggiDati, 50);
  },
  data(){
    return {
      listaEstratti: [],
      numeroDaCercare: ""
    }
  },
  methods:{
    filtra($event){
      this.numeroDaCercare = $event.target.value
    }
  }
  

}
</script>