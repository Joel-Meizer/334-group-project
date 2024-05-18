<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
                <loading-indicator :Message=message />
        </div>
        <div v-else>
            <header-text headerText="Suggested Meal Plans" subHeaderText="Discover a collection of carefully curated meal plan suggestions."/>
            <div  v-for="mealPlan in mealPlans" class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
                <meal-plans-component :headerMessage="mealPlan.name" :meals="mealPlan" />
            </div>
            <padding-item />
            <footer-file />
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const isLoading = ref(true);
const message = ref("Collecting popular meal plans...")
const mealPlans = ref([])

async function GetMealPlans() {
    try {
        const response = await fetch(`https://localhost:7249/api/MealPlan/Get`);
        const data = await response.json();
        mealPlans.value = data;
        isLoading.value = false;
    } catch (error) {
        isLoading.value = false;
        console.log(error)
    }
}

onMounted(GetMealPlans)
</script>