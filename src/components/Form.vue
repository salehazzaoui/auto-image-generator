<script setup>
import { ref } from "vue";
const prompt = ref(null);
const size = ref(null);

</script>

<template>
    <form @submit.prevent="$emit('generateImage', prompt, size)" class="flex items-center justify-center p-16">
        <div class="flex flex-col space-y-2 w-96">
            <input type="text" aria-label="prompt" name="prompt" v-model.trim="prompt" placeholder="Entre whatever you want" 
                   class="p-2 border-0 focus:outline-none">
            <select name="size" class="p-2 border-0 focus:outline-none" v-model.trim="size">
                <option selected value="small">Small</option>
                <option value="medium">Medium</option>
                <option value="large">Large</option>
            </select>
            <button type="submit" class="bg-slate-800 text-white rounded-md p-2 hover:opacity-70">Generate</button>
        </div>
    </form>
</template>