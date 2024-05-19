<template>
  
  <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 mt-8">
    <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      <li v-for="product in products" class="hoverStyling col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow">
        <div class="flex flex-1 flex-col p-8">
          <div class="flex w-full items-center justify-between space-x-6 ">
          <img class="h-40 w-50 flex-shrink-0 bg-gray-300 ml-auto mr-auto" :src="product.imageUrl" alt="" />
          </div>
          <h3 class="mt-6 text-sm font-medium text-gray-900">{{ product.name }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-500">{{ product.description }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-900">${{ product.price }}/{{ product.unitOfMeasurement }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-500">{{ product.manufacturer }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-500">Quantity per item: {{ product.weightOrQuantity }}{{ product.unitOfMeasurement }}</h3>
        </div>
        <div>
          <div v-if="accessLevel == 0 || accessLevel == 3" class="-mt-px flex divide-x divide-gray-200 bg-blue-400">
            <div class="flex w-0 flex-1">
              <div @click.prevent="addToShoppingList('individualProducts',product.id)" target=”_blank” class="text-white relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
                Add to shopping list
              </div>
            </div>
          </div>
        </div>
      </li>
      <li v-for="meal in meals" class="hoverStyling col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow">
        <div class="flex flex-1 flex-col p-8">
          <div class="flex w-full items-center justify-between space-x-6 ">
          <img class="h-40 w-50 flex-shrink-0 bg-gray-300 ml-auto mr-auto" :src="meal.imageUrl" alt="" />
          </div>
          <h3 class="mt-6 text-sm font-medium text-gray-900">{{ meal.name }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-500">{{ meal.description }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-900">${{ meal.price }}</h3>
          <h3 class="mt-1 text-sm font-medium text-gray-500">KCAL {{ meal.kcal }}</h3>
        </div>
        <div>
          <div v-if="accessLevel == 0 || accessLevel == 3" class="-mt-px flex divide-x divide-gray-200 bg-blue-400">
            <div class="flex w-0 flex-1">
              <div @click.prevent="addToShoppingList('individualMeals',meal.id)" target=”_blank” class="text-white relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
                Add to shopping list
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
  </template>
  <script setup>
  import { ref, computed } from 'vue'
  const accessLevel = computed(() => sessionStorage.getItem("334_group_user_userType"))

  const props = defineProps({
      products: Array,
      meals: Array
  });


  async function addToShoppingList(listName, itemId) {
      let itemToAdd = {}
      itemToAdd = props.products.find(x => x.id == itemId)
      if(itemToAdd == null) {
          itemToAdd = props.meals.find(x => x.id == itemId)
      }
      let body = {}
      switch(listName) {
          case "individualProducts" : {
              body = {
                  product: itemToAdd
              }
              break;
          }
          case "individualMeals" : {
              body = {
                  meal: itemToAdd
              }
              break;
          }
      }
      const listId = sessionStorage.getItem('334_group_user_shoppingListId')
      const url = `https://localhost:7249/api/ShoppingList/AddItemToList/${listId}?listName=${listName}`;
      const response = await fetch(url, {
          method: 'PUT',
          headers: {
              'Content-Type': 'application/json'
          },
          body: JSON.stringify(body)
      });

      if (response.ok) {
          console.log('Item added successfully');
      } else {
          console.error('Failed to add item', response.status);
      }
  }
  </script>

<style>
.hoverStyling {
        border-radius: 5px; 
        box-shadow: 5px 4px 8px gray;
        transition: all ease-in-out 0.3s;
    }

    .hoverStyling:hover {
        box-shadow: 6px 7px 15px gray;
    }
</style>