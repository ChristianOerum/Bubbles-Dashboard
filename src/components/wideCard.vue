<template>

    <div v-if="state == 'below'" state class="bg-gradient-to-b from-[#36393E] to-[#3E3636] rounded-xl col-span-3 row-span-1 m-2 flex flex-col justify-center items-left p-5">
        <p class="text-[#7A7D7E] text-xl font-semibold">{{ KPI_name }}</p>
            <h1 class="text-white text-3xl font-semibold">{{ KPI_value }}</h1>
            <p class="text-[#C04545] text-xl font-semibold">{{ KPI_percentage }}</p>
    </div>

    <div v-else-if="state == 'above'" state class="bg-gradient-to-b from-[#36393E] to-[#363E39] rounded-xl col-span-3 row-span-1 m-2 flex flex-col justify-center items-left p-5">
            <p class="text-[#7A7D7E] text-xl font-semibold">{{ KPI_name }}</p>
            <h1 class="text-white text-3xl font-semibold">{{ KPI_value }}</h1>
            <p class="text-[#43B14C] text-xl font-semibold">{{ KPI_percentage }}</p>
    </div>

    <div v-else-if="state == 'bubbles'" state class="bg-gradient-to-b from-[#36393E] to-[#364053] rounded-xl col-span-3 row-span-1 m-2 flex flex-col justify-center items-left p-5">
        <p class="text-[#7A7D7E] text-xl font-semibold">{{ KPI_name }}</p>
            <h1 class="text-white text-3xl font-semibold">{{ KPI_value }}</h1>
            <p class="text-[#0097ff] text-xl font-semibold">{{ KPI_percentage }}</p>
    </div>

</template>

<script>
export default {
    props: ["state","KPI_name","KPI_value","KPI_percentage"]
}
</script>