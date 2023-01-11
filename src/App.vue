<template>

  <Dashpage>
  </Dashpage>

  <button class="bg-[#43474D] right-5 bottom-5 rounded-md w-14 h-14 absolute flex flex-col justify-center items-center" @click="playSong()">
    <p class="text-white text-opacity-40 absolute w-max right-16 top-1 text-right">{{ current_song_name }}</p>
    <p class="text-white text-opacity-40 absolute w-max right-16 bottom-1 text-right">{{ current_song_artist }}</p>
    <svgCreater class="h-10 w-10" v-model:name=musicOnLable></svgCreater>

    <audio v-on:ended=songEnded() id="audio-player">
        <source src="https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Just%20the%20Two%20of%20Us%20(feat.%20Bill%20Withers).mp3?raw=true" type="audio/mp3">
    </audio>

    <audio v-on:ended=alarmEnded() id="alarm-audio-player">
        <source src="https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Alarm%20Siren%20Sound%20Fx.mp3?raw=true" type="audio/mp3">
    </audio>

  </button>

  <div v-if="popupOpen" class="transition ease-in-out absolute w-full h-screen bg-[#612020]/[0.87] top-0 flex flex-col justify-center items-center">
      <H1 class="text-[#EC2020] font-semibold text-9xl animate-pulse">ADVARSEL!</H1>
      <P class="text-[#EC2020] font-semibold text-8xl animate-pulse">Salgs afdelingen brænder!</P>
    </div>

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
      audioStarted: false,
      popupOpen: false,
      current_song_name: "Just the Two of Us",
      current_song_artist: "Bill Withers"
    }
  },

  methods: {
    playSong(){
      let audio = document.getElementById("audio-player");

      if (audio.paused){
        audio.play()
        audio.volume = 0.03
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

      let audio_options = [
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/4_00%20A.M..mp3?raw=true", name:"4:00A.M.", artist:"Taeko Ohnuki"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Aloe%20Blacc-%20The%20Man.mp3?raw=true", name:"The Man", artist:"Aloe Blacc"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/BENEE%20-%20Evil%20Spider%20(Lyric%20Video).mp3?raw=true", name:"Evil Spider", artist:"BENEE "},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Bastille%20-%20Pompeii%20(Lyrics).mp3?raw=true", name:"Pompeii", artist:"Bastille "},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Childish%20Gambino%20-%20Redbone%20(Official%20Audio).mp3?raw=true", name:"Redbone", artist:"Childish Gambino"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Dua%20Lipa%20-%20We're%20Good%20(Official%20Audio).mp3?raw=true", name:"We're Good", artist:"Dua lipa"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Everything%20She%20Wants.mp3?raw=true", name:"Everything She Wants", artist:"Wham!"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Ghost%20Town%20DJ's%20-%20My%20Boo.mp3?raw=true", name:"My Boo", artist:"Ghost town DJs"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Glass%20Animals%20-%20Heat%20Waves.mp3?raw=true", name:"Heat Waves", artist:"Glass Animals"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Gravity%20by%20John%20Mayer.mp3?raw=true", name:"Gravity", artist:"John Mayer"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/JAY-Z%20-%20Empire%20State%20Of%20Mind%20(Lyrics)%20ft.%20Alicia%20Keys.mp3?raw=true", name:"Empire state of mind", artist:"JAY-Z, Alicia Keys"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/John%20Mayer%20-%20New%20Light%20(Official%20Audio).mp3?raw=true", name:"New Light", artist:"John Mayer"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Journey%20-%20Don't%20Stop%20Believin'%20(Official%20Audio).mp3?raw=true", name:"Dont Stop Believin'", artist:"Journey"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Just%20the%20Two%20of%20Us%20(feat.%20Bill%20Withers).mp3?raw=true", name:"Just the Two of Us", artist:"Bill Withers"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Justin%20Bieber%20-%20Peaches%20ft.%20Daniel%20Caesar,%20Giveon.mp3?raw=true", name:"Peaches", artist:"Justin Beiber, Daniel Caesar"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Kali%20Uchis%20%20telepat%C3%ADa%20%5BOfficial%20Audio%5D.mp3?raw=true", name:"Telepatía", artist:"Kali Uchis"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Kings%20Of%20Leon%20-%20Use%20Somebody%20(Official%20Video).mp3?raw=true", name:"Use Somebody", artist:"Kings Of Leon"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Lil%20Nas%20X%20-%20STAR%20WALKIN'%20(Lyrics).mp3?raw=true", name:"STAR WALKIN'", artist:"Lil Nas X"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Mariya%20Takeuchi%20-%20Plastic%20Love%20(Romaji%20Lyric%20Video).vhs.mp3?raw=true", name:"Plastic Love", artist:"Mariya Takeuchi"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Maroon%205%20ft.%20Megan%20Thee%20Stallion%20-%20Beautiful%20Mistakes%20(Lyrics).mp3?raw=true", name:"Beautiful Mistakes", artist:"Maroon 5, Megan Thee Stallion"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Neonlys.mp3?raw=true", name:"Neonlys", artist:"Ukendt Kunstner"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Physical%20(Remastered%202021).mp3?raw=true", name:"Physical", artist:"Olivia Newton-John"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Post%20Malone%20-%20I%20Like%20You%20(A%20Happier%20Song)%20w.%20Doja%20Cat%20%5BOfficial%20Music%20Video%5D.mp3?raw=true", name:"I Like You", artist:"Post Malone, Doja Cat"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Private%20-%20My%20Secret%20Lover%20(High%20Quality).mp3?raw=true", name:"My Secret Lover", artist:"Private"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Stolen%20Dance.mp3?raw=true", name:"Stolen Dance", artist:"Milky Chance"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/The%20Jacksons%20-%20Blame%20It%20on%20the%20Boogie%20(Official%20Audio).mp3?raw=true", name:"Blame It on the Boogie", artist:"The Jacksons"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Toploader%20-%20Dancing%20in%20the%20Moonlight%20(Official%20Video).mp3?raw=true", name:"Dancing in the Moonlight", artist:"Toploader"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Toto%20-%20Africa%20(Official%20HD%20Video).mp3?raw=true", name:"Africa", artist:"Toto"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Treasure%20-%20Bruno%20Mars%20(Lyrics).mp3?raw=true", name:"Treasure", artist:"Bruno Mars"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/Wham!%20-%20Wake%20Me%20Up%20Before%20You%20Go-Go%20%5BLyrics%5D.mp3?raw=true", name:"Wake Me Up Before You Go-Go", artist:"Wham!"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/You.mp3?raw=true", name:"You", artist:"Regard, Troye Sivan"},
        {src: "https://github.com/ChristianOerum/Bubbles-Dashboard/blob/main/music/imugi%20%EC%9D%B4%EB%AC%B4%EA%B8%B0%20-%20Somebody%20Else%20(Official%20Video).mp3?raw=true", name:"Somebody Else", artist:"Imugi 이무기"}
      ]

      let audio = document.getElementById("audio-player");
      let selected_track = audio_options[Math.floor((Math.random()*audio_options.length))]

      audio.src = selected_track.src
      console.log("Now playing: " + selected_track.name)
      this.current_song_name = selected_track.name
      this.current_song_artist = selected_track.artist

      audio.play()
      audio.volume = 0.03
    },
    alarmEnded(){
      this.popupOpen = false
    }
  },
  mounted() {
    window.addEventListener("keypress", function(e) {
      if (String.fromCharCode(e.keyCode) == "s") {
        console.log("Run Sales alarm!")
        
        let audio = document.getElementById("alarm-audio-player");
        audio.play()
        audio.volume = 0.6
        this.popupOpen = true

      }
      else {
        //logger alle characterer som ikke er "s"
      console.log(String.fromCharCode(e.keyCode));
    }

    }.bind(this));
  }
  
});
</script>
