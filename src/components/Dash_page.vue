<template>
    <div class="bg-slate-700 w-100 h-screen flex justify-center items-center flex-col p-5">

        <div class="w-full h-full grid grid-rows-4 grid-cols-7">

          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2 flex flex-col justify-center items-center">
            <p class="text-white text-xl">Lable</p>
            <h1 class="text-white text-5xl">232</h1>
          </div>

          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2 flex flex-col justify-center items-center">
            <p class="text-white text-xl">Lable</p>
            <h1 class="text-white text-5xl">34%</h1>
          </div>

          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2 flex flex-col justify-center items-center">
            <p class="text-white text-xl">Lable</p>
            <h1 class="text-white text-5xl">...</h1>
          </div>

          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2 flex flex-col justify-center items-center">
            <p class="text-white text-xl">Lable</p>
            <h1 class="text-white text-5xl">...</h1>
          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">

          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">

          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">

          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">

          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">

          </div>
          <div class="bg-slate-800 rounded-xl col-span-1 row-span-1 m-2">
            
          </div>




        </div>

        <div class="bg-red h-{30}"> 
          <p id="test" class="text-slate-500 text-md">{{ip()}}</p>
        </div>

    </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  methods: {
    ip: function(){
      window.RTCPeerConnection = window.RTCPeerConnection || window.mozRTCPeerConnection || window.webkitRTCPeerConnection;   //compatibility for firefox and chrome
        var pc = new RTCPeerConnection({iceServers:[]}), noop = function(){};      
        pc.createDataChannel("");    //create a bogus data channel
        pc.createOffer(pc.setLocalDescription.bind(pc), noop);    // create offer and set local description
        pc.onicecandidate = function(ice){  //listen for candidate events
            if(!ice || !ice.candidate || !ice.candidate.candidate)  return;
            var myIP = /([0-9]{1,3}(\.[0-9]{1,3}){3}|[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7})/.exec(ice.candidate.candidate)[0]; 
            pc.onicecandidate = noop;
            console.log(myIP)
            //workaround fordi jeg ikke kan retunerer elmenetet direkte...
            document.getElementById("test").innerHTML="Local IP: "+ myIP + " - ssid: netværksnavn" ;
        };
  }
}
}
</script>