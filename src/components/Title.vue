<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  title: String
})
</script>
<template>
  <h2>{{ title }}</h2>
</template>

<style scoped>
h2 {
text-align: left;
font-size: 2.5rem;
  font-weight: bold;
  font-family: "Inter", sans-serif;
  color: rgb(253, 171, 139);
}
</style>
