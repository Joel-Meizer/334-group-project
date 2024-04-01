<template>
<div class="mx-auto max-w-2xl px-4 lg:max-w-4xl lg:px-0 py-12">
    <h1 class="text-2xl font-bold tracking-tight text-gray-900 sm:text-3xl pt-12">{{ headerText }}</h1>
    <p class="mt-2 text-sm text-gray-500">{{ subHeaderText }}</p>
  </div>
</template>

<script setup>
    const props = defineProps({
        headerText: String,
        subHeaderText: String
    });
</script>