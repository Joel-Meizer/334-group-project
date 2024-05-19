<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else-if="accessLevel == 1 || accessLevel == 2">
            <not-found />
        </div>
        <div v-else>
            <order-history :orders=orders />
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted, computed } from 'vue';

const orderIdList = ref([])
const orders = ref([])
const isLoading = ref(true);
const message = ref("Collecting your order history...")
const accessLevel = computed(() => sessionStorage.getItem("334_group_user_userType"))

async function GetOrderIDs() {
    try {
        const userId = sessionStorage.getItem("334_group_user_userId");
        const response = await fetch(`https://localhost:7249/api/UserAccount/Get/${userId}`);
        const data = await response.json();
        orderIdList.value = data.orderIds;

        await Promise.all(orderIdList.value.map(orderId => GetOrder(orderId)));
        
        isLoading.value = false;
    } catch (error) {
        isLoading.value = false;
        console.log(error);
    }
}

async function GetOrder(orderId) {
    try {
        const response = await fetch(`https://localhost:7249/api/Order/Get/${orderId}`);
        const data = await response.json();
        orders.value.push(data);
    } catch (error) {
        console.log(`Failed to fetch order ${orderId}:`, error);
    }
}

onMounted(GetOrderIDs)
</script>