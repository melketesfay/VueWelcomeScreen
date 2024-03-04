<script setup>
import { onBeforeMount, onMounted, ref } from 'vue'



</script>

<template>
  <div class="img-container">
    <img src="/src/assets/photos/STZH_SEB_Logo.png"/>

    <img src="/src/assets/photos/Opportunity.png"/>
    <img src="/src/assets/photos/SAG_Logo_De.png"/>
   
  </div>

</template>
<style>
.img-container {
  display: flex;
  justify-content: space-between;
  align-items: center;


  width: 100%;
  height: fit-content;
  padding: 2rem;

  background-color:  #ffffff;

  border-radius: 0.25rem;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
img{
    width: 20rem;
}
</style>
