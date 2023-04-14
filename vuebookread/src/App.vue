<script setup lang="ts">
import EBook from '@/components/EBook.vue'

</script>

<script lang="ts">
document.addEventListener('DOMContentLoaded',()=>{
  const html = document.querySelector('html')
  let fontsize=window.innerWidth/10
  fontsize=fontsize>50?50:fontsize
  html&&(html.style.fontSize = fontsize + 'px')
})
</script>

<template>
  <EBook/>
</template>

<style scoped>

</style>
