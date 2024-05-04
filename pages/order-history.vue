<template>
    <topnav />
    <order-history :orders=orders />
    <padding-item />
    <footer-file />
</template>

<script setup>

import { ref, onMounted } from 'vue';

const orders = ref([])

async function GetOrders() {
    try {
        const response = await fetch(`https://localhost:7249/api/Order/Get`);
        const data = await response.json();
        orders.value = data;
    } catch (error) {
        console.log(error)
    }
}

onMounted(GetOrders)
</script>