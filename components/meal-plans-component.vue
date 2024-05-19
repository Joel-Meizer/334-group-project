<template>
    <div class="px-6 py-6 hoverStyling">
        <div class=" border-gray-200 bg-white py-2 sm:px-6">
            <h1 class="text-base font-semibold leading-6 text-gray-900">{{headerMessage}}</h1>
        </div>
        <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <li v-for="meal in meals.meals" class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
            <div class="flex w-full items-center justify-between space-x-6 p-2">
                <img class=" w-50 flex-shrink-0 bg-gray-300 ml-auto mr-auto" :src="meal.imageUrl" alt="" />
            </div>
            <div>
            <div class="-mt-px flex divide-x divide-gray-200">
                <div class="-ml-px flex w-0 flex-1">
                <a class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
                    <h3 class="truncate text-sm font-medium text-gray-900">{{ meal.name }}:</h3>
                    <h3 class="truncate text-sm font-medium text-gray-900">{{ meal.kcal }}KCAL</h3>
                </a>
                </div>
            </div>
            </div>
        </li>
        </ul>
        <br>
        <h3 class="truncate text-sm font-medium text-gray-400">{{meals.id}}</h3><br>
        <h3 class="truncate text-sm font-semibold text-gray-900">{{meals.name}}</h3>
        <h3 class="truncate text-sm font-medium text-gray-900">{{totalCalories}}/KCAL</h3>
        <h3 class="truncate text-sm font-medium text-gray-900">${{meals.price}}</h3><br>
        <button v-if="accessLevel == 0 || accessLevel == 3" type="submit" style="min-width: 120px" @click.prevent="addToShoppingList(meals.id)" class="rounded-md bg-blue-400 mr-10 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Add to shopping list</button>
    </div>
</template>
  
<script setup>
import { defineProps, onMounted, ref, computed } from 'vue'
  const props = defineProps({
    headerMessage: String,
    meals: Object
  });

const totalCalories = ref(0)
const accessLevel = computed(() => sessionStorage.getItem("334_group_user_userType"))

function calculateCalories() {
    props.meals.meals.forEach(item =>
        totalCalories.value += item.kcal
    )
}

async function addToShoppingList(itemId) {
    let itemToAdd = props.meals
    const listId = sessionStorage.getItem('334_group_user_shoppingListId')
    const url = `https://localhost:7249/api/ShoppingList/AddItemToList/${listId}?listName=individualMealPlans`;
    const response = await fetch(url, {
        method: 'PUT',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({MealPlan: itemToAdd})
    });

    if (response.ok) {
        console.log('Item added successfully');
    } else {
        console.error('Failed to add item', response.status);
    }
}

calculateCalories()
</script>

<style>
    .hoverStyling {
        border-radius: 5px; 
        box-shadow: 5px 8px 10px gray;
        transition: all ease-in-out 0.3s;
    }

    .hoverStyling:hover {
        box-shadow: 10px 15px 15px gray;
    }
</style>