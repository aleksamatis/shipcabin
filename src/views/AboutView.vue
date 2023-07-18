<script setup>
import {computed} from 'vue'
const props = defineProps(['submitData'])

const totalCount = computed(() => {
  return  (props.submitData?.peopleCount || 0)  + (props.submitData?.petsCount || 0) + 1;
})
</script>

<template>
  <div class="about">
    <img v-if="totalCount <= 3" class="cabin-one" src="@/assets/images/a122d3.jpg">
    <img v-else class="cabin-two" src="@/assets/images/b62c2f.jpg">
  </div>
</template>

<style>
.cabin-one,.cabin-two {
  max-width: 550px;
}
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
