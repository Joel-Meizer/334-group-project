<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else>
            <header-text headerText="Trusted Grocers" subHeaderText="Take a look into our collaborative partners who induldge in our product."/>
            <trusted-grocers :stores=stores />
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const stores = ref([])
const message = ref('Collecting grocers...')
const isLoading = ref(true)

async function GetStores() {
    try {
        const response = await fetch(`https://localhost:7249/api/Grocer/Get`);
        const data = await response.json();
        stores.value = data;
        isLoading.value = false
    } catch (error) {
        console.log(error)
    }
}

onMounted(GetStores);
</script>