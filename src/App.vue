<script setup>
import {ref, computed} from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import InformationalComponent from './components/InformationalComponent.vue'

const imageData = ref()
const submitData = ref()
const pet = ref()

function onImageSelected(image) {
  imageData.value = image;
}

function onPetSelected(value) {
  pet.value = value
}

import fallbackImageUrl from '@/assets/images/pngwing.png'

const imageUrl = computed(() => {
  if (imageData.value) {
    return imageData.value
  }
  return fallbackImageUrl
})

function onSubmit(value) {
  submitData.value = value
}

</script>

<template>
  <header :class="{'with-cat': pet === 'cat' , 'with-dog': pet === 'dog' }">
    <img alt="Профиль" class="logo" :src="imageUrl" width="125" height="125" />

    <div class="wrapper">
      <InformationalComponent msg="You did it!" @image-selected="onImageSelected" @pet-selected="onPetSelected" @submit="onSubmit"/>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView :class="{'with-cat': pet === 'cat', 'with-dog': pet === 'dog'}" :submitData="submitData"/>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  width: 125px;
  height: 125px;
  border: 2px solid #000;
  border-radius: 50%;
  align-self: self-start;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
.with-cat {
  background: #3e8b3e;
}

.with-dog {
  background: #f09840;
}
</style>
