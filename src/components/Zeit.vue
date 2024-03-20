<script setup>

import { defineProps } from 'vue'
const props = defineProps({
  time: String
})

</script>


<template>
  <p>{{ time }} Uhr</p>
</template>
<style scoped>

p{
  color: rgb(250, 79, 12);
  text-align: left;
  font-size: 2.5rem;
  font-weight: bold;
  font-family: "Inter", sans-serif;
}
</style>
