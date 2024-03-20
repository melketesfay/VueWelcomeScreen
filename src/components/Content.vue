<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  content: String
})
</script>
<template>
  <p >{{ content }}</p>
</template>
<style scoped>
p {
 text-align: left;
 font-size: 2.5rem;

  font-family: "Inter", sans-serif;
  color: rgb(253, 171, 139);
}
</style>
