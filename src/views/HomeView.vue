<script setup>
import Card from '@/components/Card.vue'
import Footer from '@/components/Foot.vue'


const date = new Date();
const formattedDate = date.toLocaleDateString('de-DE', {
  year: 'numeric',
  month: '2-digit',
  day: '2-digit'
})



</script>
<template>
    <header class="title">
      <h1>Welcome to Opportunity</h1>
    <h2>{{ formattedDate }}</h2>

    </header>
  <main>

  
    <div class="cards">
      <Card />
    <Card />
    <Card />
    <Card />
    </div>
   
  </main>

</template>

<style scoped>

header{
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}
h1{
  font-size: 7rem;
  font-weight: 900;
  font-family: "Inter", sans-serif;
}
h2{
  font-size: 5rem;
  color: gray;
  font-family: "Inter", sans-serif;
}
main {
  margin-top: 2rem;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  justify-content: flex-start;
  align-items: center;


  font-family: Arial, Helvetica, sans-serif;
}

.cards{
  width: 100%;
  text-align: left;
  display: flex;
  flex-direction: column;
  gap: 2rem;

}

footer{
  margin-bottom: 0;
}
</style>
