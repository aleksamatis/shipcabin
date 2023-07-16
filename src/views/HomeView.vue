<script setup>
import TheWelcome from '../components/TheWelcome.vue'

defineProps(['submitData'])
</script>

<template>
  <main>
    <TheWelcome :submit-data="submitData"/>
  </main>
</template>
