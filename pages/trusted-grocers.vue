<template>
    <topnav />
    <header-text headerText="Trusted Grocers" subHeaderText="Take a look into our collaborative partners who induldge in our product."/>
    <trusted-grocers :stores=stores />
    <padding-item />
    <footer-file />
</template>

<script setup>

import { ref, onMounted } from 'vue';

const stores = ref([])

async function GetStores() {
    try {
        const response = await fetch(`https://localhost:7249/api/Grocer/Get`);
        const data = await response.json();
        stores.value = data;
    } catch (error) {
        console.log(error)
    }
}

onMounted(GetStores)
</script>