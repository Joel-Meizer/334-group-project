<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else>
            <header-text headerText="Items & Meals" subHeaderText="Browse through our collection of items and meals. Feel free to add them to your shopping list."/>
            <items-and-meals :products=products :meals=meals />
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const products = ref([])
const meals = ref([])
const message = ref('Collecting products and meals...')
const isLoading = ref(true)

async function GetProducts() {
    try {
        const response = await fetch(`https://localhost:7249/api/Product/Get`);
        const data = await response.json();
        products.value = data;
        await GetMeals()
        isLoading.value = false
    } catch (error) {
        console.log(error)
    }
}

async function GetMeals() {
    try {
        const response = await fetch(`https://localhost:7249/api/Meal/Get`);
        const data = await response.json();
        meals.value = data;
        isLoading.value = false
    } catch (error) {
        console.log(error)
    }
}

onMounted(GetProducts)
</script>