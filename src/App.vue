<script setup>
import Header from "./components/Header.vue"
import Form from "./components/Form.vue"
import { ref } from '@vue/runtime-core';
import axios from './utile/axios';

const imageUrl = ref(null);
const pending = ref(false);

const generateImage = async(prompt, size) => {
  pending.value = true;
  const response =  await axios.post('/openai', {
    prompt: prompt,
    size: size
  }) 
  imageUrl.value = response.data.image_url;
  pending.value = false;
}

</script>

<template>
    <Header />
    <main class="relative">
      <div v-if="pending" class="absolute top-0 left-0 w-full h-full bg-[rgba(0,0,0,0.3)]">
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
          <h1 class="text-5xl text-white font-bold">Loading...</h1>
        </div>
      </div>
      <section class="bg-amber-500">
        <Form @generate-image="(prompt, size) => generateImage(prompt, size)" />
      </section>
      <section class="bg-gray-100 p-2">
        <img class="m-auto" v-if="imageUrl" :src="imageUrl" alt="random image AI">
      </section>
    </main>
</template>

<style scoped>

</style>
