<script setup>
import { onBeforeMount, onMounted, ref, watch } from 'vue'
import Zeit from '@/components/Zeit.vue'
import Title from '@/components/Title.vue'
import Content from '@/components/Content.vue'


const sheet_id = import.meta.env.VITE_GOOGLE_SHEET_ID;
const api_token = import.meta.env.VITE_GOOGLE_API_KEY;

const zeit = ref("")
const title = ref('')
const content = ref('')
const data = ref("")




async function fetchgooglesheets(time) {
  const sheetsres = await fetch(`https://sheets.googleapis.com/v4/spreadsheets/${sheet_id}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`)
  const sheetsdata = await sheetsres.json()
  data.value = sheetsdata.valueRanges;
  zeit.value = sheetsdata.valueRanges[0].values[1][time]
  title.value = sheetsdata.valueRanges[0].values[2][time]
  content.value = sheetsdata.valueRanges[0].values[3][time]

  // console.log(sheetsdata)

}

const counter = ref('');
setInterval(() => {
  const date = new Date();
  const formattedDate = date.toLocaleDateString('de-CH', {
    year: 'numeric',
    month: '2-digit',
    day: '2-digit'
  })
  counter.value = formattedDate;
}, 1000 * 60);







onMounted(() => {
  fetchgooglesheets(0);

})

let t = 0;

watch(counter, async (newCounter, oldQuestion) => {

  fetchgooglesheets(t);
  t++;

})

</script>

<template>
  <div class="card-container">
    <Zeit :time="zeit" />
    <Title :title="title" />
    <Content :content="content" />

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

  background-color: #0F05A0;

}

@media screen and (max-width: 600px) {
  .card-container {
    padding: 2rem;
  }

}
</style>
