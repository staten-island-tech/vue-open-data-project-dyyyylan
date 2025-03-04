<template>
  <div>

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
const glah = ref('')
async function hi() {
  let res = await fetch('https://data.cityofnewyork.us/resource/25tsh-nujf.json')
  let data = await res.json();
  console.log(data);
}
onMounted(()=> {
  hi();
})
</script>

<style scoped>

</style>