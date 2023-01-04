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



      function getIPs(callback){
    var ips = [];

    var RTCPeerConnection = window.RTCPeerConnection ||
        window.webkitRTCPeerConnection || window.mozRTCPeerConnection;

    var pc = new RTCPeerConnection({
        // Don't specify any stun/turn servers, otherwise you will
        // also find your public IP addresses.
        iceServers: []
    });
    // Add a media line, this is needed to activate candidate gathering.
    pc.createDataChannel('');
    
    // onicecandidate is triggered whenever a candidate has been found.
    pc.onicecandidate = function(e) {
        if (!e.candidate) { // Candidate gathering completed.
            pc.close();
            callback(ips);
            return;
        }
        var ip = /^candidate:.+ (\S+) \d+ typ/.exec(e.candidate.candidate)[1];
        if (ips.indexOf(ip) == -1) // avoid duplicate entries (tcp/udp)
            ips.push(ip);
    };
    pc.createOffer(function(sdp) {
        pc.setLocalDescription(sdp);
    }, function onerror() {});
}

  getIPs(function(ips){
      //console.log('IPs: ', ips);
      document.getElementById("test").innerHTML = ips;
});



    }
  }
}
</script>