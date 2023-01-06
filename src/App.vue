<template>

  <Dashpage>
  </Dashpage>

  <button class="bg-[#43474D] right-5 bottom-5 rounded-md w-14 h-14 absolute flex flex-col justify-center items-center" @click="playSong()">
    <svgCreater class="h-10 w-10" v-model:name=musicOnLable></svgCreater>

    <audio v-on:ended=songEnded() id="audio-player">
        <source src="https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Just%20the%20two%20of%20us.mp3?raw=true" type="audio/mp3">
    </audio>

    <audio id="alarm-audio-player">
        <source src="https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Alarm%20Siren%20Sound%20Fx.mp3?raw=true" type="audio/mp3">
    </audio>

  </button>

</template>

<script>
//import af tailwind CSS
import './assets/tailwind.css'
//import af dash_page komponent
import Dashpage from "./page/Dash_page.vue";
import { defineComponent } from 'vue';
import svgCreater from "@/components/svgCreater.vue"; 

export default defineComponent({
  name: 'App',
  components: {
    Dashpage,
    svgCreater
  },
  data() {
    return {
      MRR: 1,
      musicOn: false,
      musicOnLable: "musicOff",
      audioStarted: false
    }
  },

  methods: {
    playSong(){
      let audio = document.getElementById("audio-player");

      if (audio.paused){
        audio.play()
        audio.volume = 0.1
        this.musicOnLable = "musicOn"
        this.musicOn = true
      }
      else {
        audio.pause()
        this.musicOnLable = "musicOff"
        this.musicOn = false
      }
    },
    songEnded(){
      let audio = document.getElementById("audio-player");
      audio.play()
    }
  },
  mounted() {
    window.addEventListener("keypress", function(e) {
      if (String.fromCharCode(e.keyCode) == "s") {
        console.log("Run Sales alarm!")
        
        let audio = document.getElementById("alarm-audio-player");
        audio.play()
        audio.volume = 0.6
      }
      else {
        //logger alle characterer som ikke er "s"
      console.log(String.fromCharCode(e.keyCode));
    }

    }.bind(this));
  }
  
});
</script>
