<script setup>
import TheWelcome from '../components/TheWelcome.vue'

defineProps(['submitData'])
</script>

<template>
  <main>
    <TheWelcome :submit-data="submitData"/>
  </main>
</template>

<style scoped>
main {
  border-left: 1px solid var(--color-border);
}
</style>
