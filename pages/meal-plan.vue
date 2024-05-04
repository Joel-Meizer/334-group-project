<template>
    <topnav />
    <header-text headerText="Suggested Meal Plans" subHeaderText="Discover a collection of carefully curated meal plan suggestions."/>
    <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
        <meal-plans headerMessage="Meal Plan 1" :meals="mealPlans" />
    </div>
    <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
        <meal-plans headerMessage="Meal Plan 2" :meals="mealPlans" />
    </div>
    <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
        <meal-plans headerMessage="Meal Plan 3" :meals="mealPlans" />
    </div>
    <padding-item />
    <footer-file />
</template>

<script setup>

import { ref, onMounted } from 'vue';

const mealPlans = ref([])

async function GetMealPlans() {
    try {
        const response = await fetch(`https://localhost:7249/api/MealPlan/Get`);
        const data = await response.json();
        mealPlans.value = data;
    } catch (error) {
        console.log(error)
    }
}

onMounted(GetMealPlans)
</script>