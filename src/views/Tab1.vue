<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <div class="tabellone">
        <header>
            <h1>{{ isNaN(estratto) ? '-': estratto}}</h1>
            <h2>{{ voce === "" ? "-" : voce["napoletano"] }}</h2>
            <h3>{{ voce === "" ? "-" : voce["italiano"] }}</h3>
        </header>
        
        <button class="panariello" @click="estrai()">
            <img :class="[ 'animate__wobble', animazione ? 'animate__animated animate__infinite': '']" src="../assets/panariello.png" alt="">
        </button>
        
        <!--ul class="estratti">
            <li class="estratto" v-for="(numero, i) in listaEstratti" :key="i">{{numero}}</li>
        </ul-->
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="js">
import Smorfia from '../dependecies/tombola-api/smorfia.json'
import { IonPage, IonContent } from '@ionic/vue';

export default  {
  name: 'Tab1',
  components: {  IonContent, IonPage },
  data(){
        return {
            animazione: false,
            estratto: NaN,
            voce: "",
            listaEstratti : []
        }
    },
    methods: {
      estrai(){
        speechSynthesis.pause()
        speechSynthesis.cancel()
        this.animazione = true
        setTimeout(()=> this.animazione = false, 1*1000)

        if (this.listaEstratti.length < 90){
            let numero = Math.floor(Math.random() * 90 + 1)
            while (this.listaEstratti.includes(numero)){
                numero = Math.floor(Math.random() * 90 + 1)
            }
            this.estratto = numero
            this.voce = Smorfia[numero.toString()]
            this.listaEstratti.unshift(numero)
            const listaEstrattiStr = JSON.stringify(this.listaEstratti)
            localStorage.setItem("estratti", listaEstrattiStr)
            const voce = Smorfia[numero.toString()]
            const frase = new SpeechSynthesisUtterance()
            frase.text = voce.napoletano
            speechSynthesis.speak(frase)
        }   
      }
    }
}
</script>


<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css');
header{
    display: grid;
    grid-template-rows: 1fr;
    place-items: center;
}
.panariello{
    background: transparent;
    outline: none !important;
    border: none !important;
    box-shadow: none !important;
    display: block;
    width: 100%;
    padding-top: 45px;
    
}
.panariello img{
    width: 250px;
    --animate-duration: 1s;
}
/*
.tabellone{
    display: grid;
    grid-template-rows: repeat(3, 1fr);
   
}*/
h1, h2, h3{
    margin: 0;
}
.estratti{
    list-style: none;
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: repeat(9, 1fr);
    row-gap: 5px;
    column-gap: 5px;
    padding: 0;
    min-width: 336px;
}

h1,
.estratto{
    --dim : 42px;
    padding: 3px;
    height: var(--dim);
    width: var(--dim);
    background-color: var(--panna);
    color: var(--rosso);
    border: 4px solid var(--rosso);
    border-radius: 50%;
    box-sizing: border-box;
    place-content: center;
    display: grid;
    place-content: center;
    display: grid;
    font-weight: 700;
    box-shadow: inset 0px 1px 1px 1px rgba(0,0,0,0.5);
    text-shadow: -1px 1px 1px rgba(0,0,0,0.5);
}

h1{
    --dim : 72px;
    margin-top: 30px;
    margin-bottom: 30px;
    border-width: 6px;
}

h2, h3{
    color: white;
}

h3{
    text-align: center;
    font-size: 16px;
    font-style: italic;
}
</style>