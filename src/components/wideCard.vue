<template>

    <div class="bg-gradient-to-b from-[#36393E] to-[#434343] rounded-xl col-span-3 row-span-1 m-2 justify-center items-left grid grid-rows-1 pl-5 pr-5 grid-cols-5">

        <div class="rounded-xl col-span-1 row-span-1 flex flex-col justify-center items-center">
                <p class="text-[#7A7D7E] text-2xl font-semibold">Antal skoler</p>
                <h1 class="text-white text-5xl font-semibold">120</h1>
            </div>

        <div class="rounded-xl col-span-1 row-span-1 flex flex-col justify-center items-center">
            <p class="text-[#7A7D7E] text-2xl font-semibold">Antal Kommuner</p>
            <h1 class="text-white text-5xl font-semibold">120</h1>
        </div>

        <div class="rounded-xl col-span-1 row-span-1 flex flex-col justify-center items-center">
                <p class="text-[#7A7D7E] text-2xl font-semibold">Antal brugere</p>
                <h1 class="text-white text-5xl font-semibold">120</h1>
            </div>

        <div class="rounded-xl col-span-2 row-span-1 flex flex-col justify-center items-center relative">
            <p class="text-[#7A7D7E] text-2xl font-semibold">Markedsandele</p>
            <h1 class="text-white text-5xl font-semibold">120</h1>
            <svgCreater class="h-full w-full absolute" name="DK"></svgCreater>
        </div>


    </div>

</template>

<script>

import svgCreater from "@/components/svgCreater.vue"; 

export default {
  name: 'App',
  components: {
    svgCreater
  },
  methods: {}
}
</script>