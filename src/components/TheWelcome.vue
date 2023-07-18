<script setup>
import DocumentationIcon from './icons/IconDocumentation.vue'
import SupportIcon from './icons/IconSupport.vue'

const props = defineProps(['submitData'])
</script>

<template>
  <div class="general">
    <div class="documentation-image">
      <DocumentationIcon />
    </div>
    <div class="details">
      <h3>Подробности</h3>
      <div class="details-str">
      <div>С вами в каюте едет <div class="details-special">{{ props.submitData?.petsCount }}</div> питомца, <div class="details-special">{{ props.submitData?.peopleCount }}</div> человек и Вы.</div>
      </div>
    </div>
  </div>
  <div class="general">
    <div class="documentation-image">
      <SupportIcon/>
    </div>
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

.details-special {
  width: 45px;
  height: 45px;
  background: #419152;
  border-radius: 4px;
  border: 1px solid #59be6e;
  display: inline-block;
  vertical-align: middle;
  text-align: center;
  font-size: 20px;
  padding-top: 3px;
  color: #fff;
}

/* .details-str {
  display: inline;
  vertical-align: middle;
  line-height: 100px;
} */
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