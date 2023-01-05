<template>
    <div class="bg-[#282B30] w-100 h-screen flex flex-col justify-center items-center flex-col p-10">

        <div class="w-full h-full grid grid-rows-4 grid-cols-5">
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="MRR" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="ARR" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="CLV" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Opsalg MRR" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Lukkede handler værdi" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="CAC" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="CAC Payback" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="CAC/CLV" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Antal salg/måned" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Skoler lukket udfra mål" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Churn Rate" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Revenue Churn Rate (ARR%)" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Revenue Churn Rate (Churn + UP)" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Booket demo" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="Afholdt demo" KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="K.G. mellem B.D. og A.D." KPI_percentage="23%"></reusableCard>
          <reusableCard state="above" KPI_value="100.000 DKK" KPI_name="K.G. mellem B.D. og Salg" KPI_percentage="23%"></reusableCard>
          <wideCard></wideCard>

        </div>

    </div>
</template>

<script>

import reusableCard from "@/components/reusableCard.vue"; 
import wideCard from "@/components/wideCard.vue"; 

export default {
  name: 'App',
  components: {
    reusableCard,
    wideCard
  },
  methods: {
    //calls all api's
    DataAPICall: function(){
      console.log("hi")
    }
  },
  //on page load, run func
  beforeMount(){
    this.DataAPICall()
 },
}
</script>