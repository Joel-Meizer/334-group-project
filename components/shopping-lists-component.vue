<template>
    <div v-if="isLoading">
        <loading-indicator :Message=message />
    </div>
    <main v-else class="py-24">
        <div class="mx-auto max-w-7xl sm:px-2 lg:px-8">
            <div class="mx-auto max-w-2xl px-4 lg:max-w-4xl lg:px-0">
            <h1 class="text-2xl font-bold tracking-tight text-gray-900 sm:text-3xl">{{shoppingListItems.displayName}}</h1>
            <p class="mt-2 text-sm text-gray-500">View your shopping list. Manage what items exist in your list and use it to create your next orders.</p>
            </div>
        </div>
        <ul role="list" class="divide-y divide-gray-100 px-10 mt-16" style="box-sizing: 4px 4px 8px 10px black;">
            <li class="flex justify-between gap-x-6 bg-gray-900 text-white-900 px-4" style="height: 30px; line-height: 30px;">
                <div class="flex min-w-0 gap-x-4">
                    <p class="h-12 w-12 flex-none rounded-full"></p>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Item name: </p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Item Price: </p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Item Description: </p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Item ID: </p>
                    </div>
                </div>
            </li>
            <li class="flex justify-between gap-x-6 bg-gray-900 px-4" style="height: 30px; line-height: 30px;">
                <div class="flex min-w-0 gap-x-4">
                    <p class="h-12 w-12 flex-none rounded-full"></p>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Individual Items:</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                </div>
            </li>
            <li v-for="item in shoppingListItems.individualProducts" class="hover flex justify-between gap-x-6 py-5 px-4">
                <div class="flex min-w-0 gap-x-4">
                    <img class="h-12 w-12 flex-none rounded-full bg-gray-50" :src="item.imageUrl" alt="" />
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.name }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">${{ item.price }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.description }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.id }}</p>
                    </div>
                </div>
                <div v-if="accessLevel == 0 || accessLevel == 3" class="hidden shrink-0 sm:flex sm:flex-col sm:items-end">
                    <button type="submit" @click.prevent="deleteItem(shoppingListId, 'individualProducts', item.id)" class="rounded-md bg-red-400 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Remove Item</button>
                </div>
            </li>
            <li class="flex justify-between gap-x-6 bg-gray-900" style="height: 30px; line-height: 30px;">
                <div class="flex min-w-0 gap-x-4">
                    <p class="h-12 w-12 flex-none rounded-full"></p>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Meals:</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                </div>
            </li>
            <li v-for="item in shoppingListItems.individualMeals" class="hover flex justify-between gap-x-6 py-5 px-4">
                <div class="flex min-w-0 gap-x-4">
                    <img class="h-12 w-12 flex-none rounded-full bg-gray-50" :src="item.imageUrl" alt="" />
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.name }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">${{ item.price }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.description }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.id }}</p>
                    </div>
                </div>
                <div v-if="accessLevel == 0 || accessLevel == 3" class="hidden shrink-0 sm:flex sm:flex-col sm:items-end">
                    <button type="submit" @click.prevent="deleteItem(shoppingListId, 'individualMeals', item.id)" class="rounded-md bg-red-400 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Remove Item</button>
                </div>
            </li>
            <li class="flex justify-between gap-x-6 bg-gray-900" style="height: 30px; line-height: 30px;">
                <div class="flex min-w-0 gap-x-4">
                    <p class="h-12 w-12 flex-none rounded-full"></p>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Meal Plans:</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900"></p>
                    </div>
                </div>
            </li>
            <li v-for="item in shoppingListItems.individualMealPlans" class="hover flex justify-between gap-x-6 py-5 px-4">
                <div class="flex min-w-0 gap-x-4">
                    <img class="h-12 w-12 flex-none rounded-full bg-gray-50" :src="item.imageUrl" alt="" />
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.name }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">${{ item.price }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.description }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-900">{{ item.id }}</p>
                    </div>
                </div>
                <div v-if="accessLevel == 0 || accessLevel == 3" class="hidden shrink-0 sm:flex sm:flex-col sm:items-end">
                    <button type="submit" @click.prevent="deleteItem(shoppingListId, 'individualMealPlans', item.id)" class="rounded-md bg-red-400 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Remove Item</button>
                </div>
            </li>
            <li class="flex justify-between gap-x-6 py-5 bg-gray-900">
                <div class="flex min-w-0 gap-x-4">
                    <p class="h-12 w-12 flex-none rounded-full "></p>
                    <button v-if="accessLevel == 0 || accessLevel == 3" type="submit" style="min-width: 120px" @click.prevent="createOrder()" class="rounded-md bg-blue-400 mr-10 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Submit Order</button>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                        <p class="text-sm font-semibold leading-6 text-gray-400">Total Amount: </p>
                        <p class="text-sm font-semibold leading-6 text-gray-400">${{ totalAmount }}</p>
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 280px; max-width: 280px">
                    </div>
                    <div class="min-w-0 flex-auto mr-10" style="min-width: 120px; max-width: 120px">
                    </div>
                </div>
            </li>
        </ul>
    </main>
  </template>
  
  <script setup>
  import {ref,onMounted,computed} from 'vue'
  const shoppingListItems = ref([])
  const shoppingListId = ref("")
  const totalAmount = ref(0)
  const isLoading = ref(true)
  const message = ref("Generating shopping list...")
  const accessLevel = computed(() => sessionStorage.getItem("334_group_user_userType"))

  async function getShoppingList(shoppingListId) {
    const response = await fetch("https://localhost:7249/api/ShoppingList/Get/" + shoppingListId)
    shoppingListItems.value = await response.json();
    calculateCost();
  }

  async function getShoppingListId() {
    const userId = sessionStorage.getItem("334_group_user_userId")
    const response = await fetch("https://localhost:7249/api/UserAccount/Get/" + userId)
    const userObj = await response.json();
    shoppingListId.value = userObj.relatedShoppingListId
    if(userObj.relatedShoppingListId != null) {
        await getShoppingList(userObj.relatedShoppingListId)
    }
  }

function calculateCost() {
  let total = 0
  
  if (shoppingListItems.value.individualProducts) {
    shoppingListItems.value.individualProducts.forEach(item => {
      total += item.price
    })
  }

  if (shoppingListItems.value.individualMeals) {
    shoppingListItems.value.individualMeals.forEach(meal => {
      total += meal.price
    })
  }

  if (shoppingListItems.value.individualMealPlans) {
    shoppingListItems.value.individualMealPlans.forEach(plan => {
      total += plan.price
    })
  }

  totalAmount.value = total.toFixed(2)
  isLoading.value = false
}

async function deleteItem(listId, listName, itemId) {
    const url = `https://localhost:7249/api/ShoppingList/DeleteItemFromList/${listId}?listName=${listName}&itemId=${itemId}`;
    const response = await fetch(url, {
        method: 'DELETE'
    });

    if (response.ok) {
        console.log('Item deleted successfully');
        message.value = "Successfully deleted item, reloading shopping list..."
        window.location.reload()
    } else {
        console.error('Failed to delete item', response.status);
    }
}

async function createOrder() {
    const body = {
        id: "",
        TotalPrice: totalAmount.value,
        OrderName: shoppingListItems.value.displayName,
        OrderDate: new Date(),
        IsDelivered: false,
        Status: "Pending confirmation",
        deliveryAddress: "example address",
        ShoppingList: shoppingListItems.value
    }

    const url = `https://localhost:7249/api/Order/Post`;
    const response = await fetch(url, {
        method: 'POST',
        body: JSON.stringify(body),
        headers: {
            'Content-Type': 'application/json'
        },
    });

    const data = await response.json()
    const userId = sessionStorage.getItem("334_group_user_userId")
    const url2 = 'https://localhost:7249/api/UserAccount/UpdateOrderIDs/' + userId + "?orderId=" + data.id;
    await fetch(url2, {
        method: 'PUT'
    });
}

  onMounted(getShoppingListId)
  </script>

<style>
.hover {
    transition: all ease-in-out 0.2s;
}

.hover:hover {
    background-color: rgb(240, 240, 240);
}
</style>