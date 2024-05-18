<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else>
            <shopping-lists-component />
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const shoppingListItems = ref([])
const isLoading = ref(true);
const message = ref("Collecting your shopping list data...")

async function GetShoppingList() {
    try {
        const response = await fetch(`https://localhost:7249/api/ShoppingList/Get`);
        const data = await response.json();
        shoppingListItems.value = data;
        isLoading.value = false
    } catch (error) {
        isLoading.value = false
        console.log(error)
    }
}

onMounted(GetShoppingList)
</script>