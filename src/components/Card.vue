<script setup>
import { onBeforeMount, onMounted, onUnmounted, ref,watch } from 'vue'
import Zeit from '@/components/Zeit.vue'
import Title from '@/components/Title.vue'
import Content from '@/components/Content.vue'


const sheet_id = import.meta.env.VITE_GOOGLE_SHEET_ID;
const api_token = import.meta.env.VITE_GOOGLE_API_KEY;

const zeit = ref("")
const title = ref('')
const content = ref('')
const data = ref("")

let dateCounter = ref("");
let columnCounter = ref(0);

setInterval(() => {
  const date = new Date();
const formattedDate = date.toLocaleDateString('de-DE', {
  year: 'numeric',
  month: '2-digit',
  day: '2-digit'
  // hour: '2-digit',
  // minute:'2-digit',
  // second:'2-digit'
})

dateCounter.value = formattedDate.split(".")[0];
// console.log(dateCounter.value)
}, 100);


var googleData = []


async function fetchgooglesheets() {
  const sheetsres = await fetch(`https://sheets.googleapis.com/v4/spreadsheets/${sheet_id}/values:batchGet?ranges=A1%3AH100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`)
  const sheetsdata = await sheetsres.json()
  data.value = sheetsdata.valueRanges;
  zeit.value = sheetsdata.valueRanges[0].values[1][0]
  title.value = sheetsdata.valueRanges[0].values[1][2]
  content.value = sheetsdata.valueRanges[0].values[2][2]


  let dta = sheetsdata.valueRanges[0].values;
  console.log(dta[0])

  for (let i = 0; i < dta.length; i++) {
    
    googleData.push(dta[i]);
    // console.log(dta[i])
    
  }

  

}

fetchgooglesheets();


setTimeout(() => {
  for (let i = 0; i < googleData[0].length; i++) {
    if (googleData[0][i].split(".")[0]==dateCounter.value) {

      // googleData[0][i].split(".")[0]==dateCounter
      console.log(`dateCounter is: ${dateCounter.value} and google date is:${googleData[0][i]}`)
      return
    }
    
  }

  
}, 1000);

    
  console.log(dateCounter.value)




watch(dateCounter,(newCounter)=>{
  // console.log(`newCounter is: ${newCounter}`)
})

let fetchInterval;

onMounted(() => {

  fetchInterval = setInterval(() => {
    fetchgooglesheets();
  }, 1000*60*30);
  

})


onUnmounted(()=>{
  clearInterval(fetchInterval)
})

</script>

<template>
  <div class="card-container">
    <Zeit :time="zeit"/>
    <Title :title="title"/>
    <Content :content="content"/>
   
  </div>

</template>
<style>
.card-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
 

  width: 100%;
  height: fit-content;
  padding: 3rem;

  background-color:  #0F05A0;

}
@media screen and (max-width: 600px) {
  .card-container{
    padding: 2rem;
  }

}
</style>
