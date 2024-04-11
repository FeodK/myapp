<script setup>
defineProps({
    title: String,
    description: String,
    imageUrl: String
})
</script>
<template>
    <div class="flex flex-col items-center text-center w-72 mx-auto">
        <img class="h-20 h-20" :src="imageUrl" alt="Info image">
        <h2 class="m-4 text-2xl font-medium">{{ title }}</h2>
        <p class="text-gray-400">{{ description }}</p>
    </div>
</template>