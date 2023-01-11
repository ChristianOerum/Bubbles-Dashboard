<template>
    <div class="bg-[#282B30] w-100 h-screen flex flex-col justify-center items-center flex-col p-10">

        <div class="w-full h-full grid grid-rows-4 gap-2 grid-cols-5">
          <reusableCard state="above" :KPI_value=mrr KPI_name="MRR" :KPI_percentage=mrrP></reusableCard>
          <reusableCard state="above" :KPI_value=arr KPI_name="ARR" :KPI_percentage=arrP></reusableCard>
          <reusableCard state="above" :KPI_value=clv KPI_name="CLV" :KPI_percentage=clvP></reusableCard>
          <reusableCard state="above" :KPI_value=opsalg_CLV KPI_name="Opsalg MRR" :KPI_percentage=opsalg_CLVP></reusableCard>
          <reusableCard state="above" :KPI_value=lukkede_Handler_Værdi KPI_name="Lukkede handler værdi" :KPI_percentage=lukkede_Handler_VærdiP></reusableCard>
          <reusableCard state="above" :KPI_value=cac KPI_name="CAC" :KPI_percentage=cacP></reusableCard>
          <reusableCard state="above" :KPI_value=cacPayback KPI_name="CAC Payback" :KPI_percentage=cacPaybackP></reusableCard>
          <reusableCard state="above" :KPI_value=cac_clv KPI_name="CLV/CAC" :KPI_percentage=cac_clvP></reusableCard>
          <reusableCard state="above" :KPI_value=antal_salg_Måned KPI_name="Antal salg/måned" :KPI_percentage=antal_salg_MånedP></reusableCard>
          <reusableCard state="above" :KPI_value=antal_salg_Mål KPI_name="Skoler lukket udfra mål" :KPI_percentage=antal_salg_MålP></reusableCard>
          <reusableCard state="above" :KPI_value=chrun_Rate KPI_name="Churn Rate" :KPI_percentage=chrun_RateP></reusableCard>
          <reusableCard state="above" :KPI_value=revenue_Chrun_Rate_ARR KPI_name="Revenue Churn Rate (ARR%)" :KPI_percentage=revenue_Chrun_Rate_ARRP></reusableCard>
          <reusableCard state="above" :KPI_value=revenue_Chrun_Rate_UP KPI_name="Revenue Churn Rate (Churn + UP)" :KPI_percentage=revenue_Chrun_Rate_UPP></reusableCard>
          <reusableCard state="above" :KPI_value=booket_demo KPI_name="Booket demo" :KPI_percentage=booket_demoP></reusableCard>
          <reusableCard state="above" :KPI_value=afholdt_demo KPI_name="Besøgte skoler" :KPI_percentage=afholdt_demoP></reusableCard>
          <reusableCard state="above" :KPI_value=konvetering_1 KPI_name="K.G. mellem B.D. og A.D." :KPI_percentage=konvetering_1P></reusableCard>
          <reusableCard state="above" :KPI_value=konvetering_2 KPI_name="K.G. mellem B.D. og Salg" :KPI_percentage=konvetering_2P></reusableCard>
          <wideCard :skoler=antal_skoler blank1="b1" :kommuner=antal_kommuner blank2="b2" :brugere=antal_brugerer blank3="b3" :ialt=markedsandel></wideCard>

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
  data() {
    return {
      mrr: "🚀",
      arr: "🚀",
      clv: "🚀",
      opsalg_CLV: "🚀",
      lukkede_Handler_Værdi: "🚀",
      cac: "🚀",
      cacPayback: "🚀",
      cac_clv: "🚀",
      antal_salg_Måned: "🚀",
      antal_salg_Mål: "🚀",
      chrun_Rate: "🚀",
      revenue_Chrun_Rate_ARR: "🚀",
      revenue_Chrun_Rate_UP: "🚀",
      booket_demo: "🚀",
      afholdt_demo: "🚀",
      konvetering_1: "🚀",
      konvetering_2: "🚀",
      antal_skoler: "🚀",
      antal_kommuner: "🚀",  
      antal_brugerer: "🚀",  
      markedsandel: "🚀",

      mrrP: "0%",
      arrP: "0%",
      clvP: "0%",
      opsalg_CLVP: "0%",
      lukkede_Handler_VærdiP: "0%",
      cacP: "0%",
      cacPaybackP: "0%",
      cac_clvP: "0%",
      antal_salg_MånedP: "0%",
      antal_salg_MålP: "0%",
      chrun_RateP: "0%",
      revenue_Chrun_Rate_ARRP: "0%",
      revenue_Chrun_Rate_UPP: "0%",
      booket_demoP: "0%",
      afholdt_demoP: "0%",
      konvetering_1P: "0%",
      konvetering_2P: "0%"

    }
  },
  methods: {
    //calls all api's
    LoadDataFromBackend: async function(){

      setInterval(async () => {

      const companyUrl = "bubblesaps"
      const token = "b8e12906a11c6c9ba7eeae923e5f23a54adab5d1";
      const limit = "500"

      let start = 0
      let tempArr = []
      let MRR = 0
      let CLV = 0
      let CLV_count = 0
      let Opsalg_MRR = 0
      let LHV = 0
      let google_sheetData = 0
      let salg_DM = 1
      let antalSkoler = 0
      let antalKommuner = 0
      let antalBrugere = 0
      let markdsStørrelse = 0
      let bookedDemo = 0
      let afholdtDemo = 0
      let samlet_antal_salg = 0


      while (tempArr.length == start) {
          let url = `https://${companyUrl}.pipedrive.com/api/v1/deals?start=${start}&limit=${limit}&api_token=${token}`
          console.log(url)
          await fetch(url)
          .then((response) => response.json())
          .then((data) => {
              tempArr.push(...data.data)
              console.log(tempArr)
              start += 500
          })
          }

          for (let i = 0; i < tempArr.length; i++) {
              //MRR
              if(tempArr[i].value != 0 && tempArr[i].status == "won" ){
                  MRR += tempArr[i].fc934713f91688605b3c516dc29de0a897a865bf
              }  

              //CLV + lukkede handler værdi + salg denne måned
              if (tempArr[i].status == "won") {
                  CLV += tempArr[i].value
                  CLV_count += 1

                  LHV += tempArr[i].value

                  samlet_antal_salg += 1

                  if(tempArr[i].close_time == (new Date()).getMonth() + 1) {
                      salg_DM += 1 
                  }
              }
              
              //Opsalg MRR
              if (tempArr[i].status == "won" && tempArr[i]["41bf727b06a597ee86020f7b240b88cc02ec9a74"] == "24" && tempArr[i].first_won_time ==  (new Date()).getMonth() + 1) {
                  Opsalg_MRR += tempArr[i].fc934713f91688605b3c516dc29de0a897a865bf
              }

          } 

          //google sheet data.
          await fetch("https://docs.google.com/spreadsheets/d/1-HhNg6BcIrBGFkqS0sgMYrX-6BI_G6tutCURuajqEjQ/edit?usp=sharing")
              .then(response => response.text())
              .then(data => {
                  const rows = data.split('\n').slice(1);
                  const temp_strToArr = (rows[2].split('"'))[0]
                  google_sheetData = temp_strToArr.split(",")

                  antalSkoler = google_sheetData[3]
                  antalKommuner = google_sheetData[4]
                  antalBrugere = google_sheetData[5]
                  markdsStørrelse = google_sheetData[6]
                  bookedDemo = google_sheetData[7]
                  afholdtDemo = google_sheetData[8]
          })

          this.mrr = MRR.toLocaleString() + " DKK"
          console.log("MRR= " + MRR)

          this.arr = (MRR*12).toLocaleString() + " DKK"
          console.log("ARR= " + (MRR*12))
          
          this.clv = (CLV/CLV_count).toLocaleString() + " DKK"
          console.log("CLV= " + (CLV/CLV_count))

          this.opsalg_CLV = Opsalg_MRR.toLocaleString() + " DKK"
          console.log("Opsalg_MRR= " + Opsalg_MRR)

          this.lukkede_Handler_Værdi = LHV.toLocaleString() + " DKK"
          console.log("Lukkede handler værdi= " + LHV)

          this.cac = google_sheetData[0].toLocaleString() + " DKK"
          console.log("CAC= " + google_sheetData[0])

          this.cacPayback = (google_sheetData[0]/(MRR/samlet_antal_salg)).toFixed(1) + " Mdr."
          console.log("CACPayback= " + (google_sheetData[0]/(MRR/samlet_antal_salg)).toFixed(1) + " Mdr.")

          this.cac_clv = "x" + ((CLV/CLV_count)/Number(google_sheetData[0])).toFixed(2)
          console.log("CAC/CLV= " + ((CLV/CLV_count)/Number(google_sheetData[0])))

          this.antal_salg_Måned = salg_DM
          console.log("Antal salg/måned= " + salg_DM)

          this.antal_salg_Mål = ((salg_DM/google_sheetData[2])*100).toFixed(1) + "%"
          console.log("Antal salg/mål= " + ((salg_DM/google_sheetData[2])*100).toFixed(1) + "%" )

          this.chrun_Rate = 0
          console.log("Churn rate?")

          this.revenue_Chrun_Rate_ARR = 0
          console.log("Revenue Churn Rate (ARR%)?")

          this.revenue_Chrun_Rate_UP = 0
          console.log("Revenue Churn Rate (Churn + UP)?")

          this.booket_demo = bookedDemo
          console.log("Booket demo= " + bookedDemo)

          this.afholdt_demo = afholdtDemo
          console.log("Afholdt demo= " + afholdtDemo)

          this.konvetering_1 = ((afholdtDemo/bookedDemo)*100).toFixed(1) + "%"
          console.log("K.G. mellem B.D. og A.D= " + ((afholdtDemo/bookedDemo)*100).toFixed(1) + "%")

          this.konvetering_2 = ((salg_DM/bookedDemo)*100).toFixed(1) + "%"
          console.log("K.G. mellem B.D. og Salg= " + ((salg_DM/bookedDemo)*100).toFixed(1) + "%")

          this.antal_skoler = antalSkoler
          console.log("Antal skoler= " + antalSkoler)

          this.antal_kommuner = antalKommuner
          console.log("Antal Kommuner= " + antalKommuner)

          this.antal_brugerer = antalBrugere
          console.log("Antal brugere= " + antalBrugere)

          this.markedsandel = ((antalSkoler/markdsStørrelse)*100).toFixed(2) + "%"
          console.log("Markedsandele= " + ((antalSkoler/markdsStørrelse)*100).toFixed(2) + "%")


          console.log("_______________")
        console.log("data interval ran")
      }, 10000);

    }
  },
  //on page load, run func
  beforeMount(){
    this.LoadDataFromBackend()
 },
}
</script>