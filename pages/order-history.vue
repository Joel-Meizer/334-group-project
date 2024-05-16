<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else>
            <order-history :orders=orders />
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const orders = ref([])
const isLoading = ref(true);
const message = ref("Collecting your order history...")

async function GetOrders() {
    try {
        const response = await fetch(`https://localhost:7249/api/Order/Get`);
        const data = await response.json();
        orders.value = data;
        isLoading.value = false
    } catch (error) {
        isLoading.value = false
        console.log(error)
    }
}

onMounted(GetOrders)
</script>