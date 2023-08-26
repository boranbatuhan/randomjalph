<template>
  
  <div class="container mx-auto ">
    <router-view v-if="showRouter"></router-view>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const showRouter=ref(false)
onMounted(()=>{
  document.fonts.load('1rem "japan-wave"').then(()=>{
    showRouter.value=true
  })
})
</script>

<style scoped>

</style>