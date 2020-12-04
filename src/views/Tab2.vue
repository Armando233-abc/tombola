<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Numeri estratti</ion-title>
      </ion-toolbar>
      <ion-searchbar placeholder="Cerca numero" @input="filtra($event)"></ion-searchbar>
    </ion-header>
    <ion-content>     
      <ion-list>
          <ion-item v-for="(numero, i) in listaEstratti" :key="i">
            <span class="estratto" slot="start">{{numero}}</span>  
            <ion-label>
              <h2 class="napoletano">{{napoletano(numero)}}</h2>
              <h5>{{italiano(numero)}}</h5>
            </ion-label>
          </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import Smorfia from '../dependecies/tombola-api/smorfia.json'

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
    },
    napoletano(numero){
      return Smorfia[numero.toString()]["napoletano"]
    },
    italiano(numero){
      return Smorfia[numero.toString()]["italiano"]
  
    }
  }
}
</script>

<style>

  ion-list h2.napoletano{
    font-weight: bold;
  }
  ion-list h5{
    color: var(--panna);
  }

  
</style>