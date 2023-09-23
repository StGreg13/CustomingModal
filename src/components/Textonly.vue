<script setup lang="ts">
import { ref } from 'vue';
defineProps<{
  header: string
  text: string
}>();
const count = ref(0);
</script>

<template>
  <div class="container">

    <div class="main">
      <p>{{text}}</p>
    </div>
  </div>
</template>

<style scoped>

</style>
