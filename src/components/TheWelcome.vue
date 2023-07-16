<script setup>
import DocumentationIcon from './icons/IconDocumentation.vue'
import SupportIcon from './icons/IconSupport.vue'

const props = defineProps(['submitData'])
</script>

<template>
  <div class="general">
    <DocumentationIcon class="documentation-image"/>
    <div class="details">
      <h3>Подробности</h3>
      <div>С вами в каюте едет {{ props.submitData?.petsCount }} питомца, {{ props.submitData?.peopleCount }} человек и Вы.</div>
    </div>
  </div>
  <div class="general">
  <SupportIcon class="documentation-image"/>
  </div>
</template>
<style scoped>
.general {
  margin-top: 0;
  padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
}
.details {
  flex: 1;
  margin-left: 1rem;
}
.documentation-image {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;
  color: var(--color-text);
}

h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

@media (min-width: 1024px) {

  .documentation-image {
    top: calc(50% - 25px);
    left: -26px;
    position: absolute;
    border: 1px solid var(--color-border);
    background: var(--color-background);
    border-radius: 8px;
    width: 50px;
    height: 50px;
  }
}
</style>