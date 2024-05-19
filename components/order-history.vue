<template>
    <div class="bg-white">
      <main class="py-24">
        <div class="mx-auto max-w-7xl sm:px-2 lg:px-8">
          <div class="mx-auto max-w-2xl px-4 lg:max-w-4xl lg:px-0">
            <h1 class="text-2xl font-bold tracking-tight text-gray-900 sm:text-3xl">Order history</h1>
            <p class="mt-2 text-sm text-gray-500">Check the status of recent orders, manage returns, and discover similar products.</p>
          </div>
        </div>
  
        <section aria-labelledby="recent-heading" class="mt-16">
          <h2 id="recent-heading" class="sr-only">Recent orders</h2>
          <div class="mx-auto max-w-7xl sm:px-2 lg:px-8">
            <div class="mx-auto max-w-2xl space-y-8 sm:px-4 lg:max-w-4xl lg:px-0">
              <div v-for="order in orders" :key="order.id" class="border-b border-t border-gray-200 bg-white shadow-sm sm:rounded-lg sm:border">
                <h3 class="sr-only">
                  Order placed on <time :datetime="order.orderDate">{{ order.orderDate }}</time>
                </h3>
  
                <div class="flex items-center border-b border-gray-200 p-4 sm:grid sm:grid-cols-4 sm:gap-x-6 sm:p-6">
                  <dl class="grid flex-1 grid-cols-2 gap-x-20 text-sm sm:col-span-3 sm:grid-cols-3 lg:col-span-2">
                    <div>
                      <dt class="font-medium text-gray-900">Order number</dt>
                      <dd class="mt-1 text-gray-500" style="max-width: 100px;">{{ order.id }}</dd>
                    </div>
                    <div class="hidden sm:block">
                      <dt class="font-medium text-gray-900">Date placed</dt>
                      <dd class="mt-1 text-gray-500">
                        <time :datetime="order.orderDate">{{ getLocalTime(order.orderDate) }}</time>
                      </dd>
                    </div>
                    <div>
                      <dt class="font-medium text-gray-900">Total amount</dt>
                      <dd class="mt-1 font-medium text-gray-900">${{ order.totalPrice }}</dd>
                    </div>
                  </dl>
  
                  <Menu as="div" class="relative flex justify-end lg:hidden">
                    <div class="flex items-center">
                      <MenuButton class="-m-2 flex items-center p-2 text-gray-400 hover:text-gray-500">
                        <span class="sr-only">Options for order {{ order.number }}</span>
                        <EllipsisVerticalIcon class="h-6 w-6" aria-hidden="true" />
                      </MenuButton>
                    </div>
                  </Menu>
                </div>
  
                <!-- Products -->
                <h4 class="sr-only">Items</h4>
                <ul role="list" class="divide-y divide-gray-200">
                  <li  class="p-4 sm:p-6">
                    <div class="flex items-center sm:items-start">
                      <div class="h-20 w-20 flex-shrink-0 overflow-hidden rounded-lg bg-gray-200 sm:h-40 sm:w-40">
                        <img src="https://images.pexels.com/photos/868110/pexels-photo-868110.jpeg?auto=compress&cs=tinysrgb&w=1000&h=750&dpr=1" class="h-full w-full object-center" />
                      </div>
                      <div class="ml-6 flex-1 text-sm">
                        <div class="font-medium text-gray-900 sm:flex sm:justify-between">
                          <h5>{{ order.shoppingList.displayName }}</h5>
                          <p class="mt-2 sm:mt-0">${{ order.totalPrice }}</p>
                        </div>
                        <p v-for="item in order.shoppingList.individualProducts" class="hidden text-gray-500 sm:mt-2 sm:block">{{ item.name }} ${{ item.price }}/{{ item.unitOfMeasurement }}</p>
                        <p v-for="item in order.shoppingList.individualMeals" class="hidden text-gray-500 sm:mt-2 sm:block">{{ item.name }} ${{ item.price }}</p>
                        <p v-for="item in order.shoppingList.individualMealPlans" class="hidden text-gray-500 sm:mt-2 sm:block">{{ item.name }} ${{ item.price }}</p>
                      </div>
                    </div>
  
                    <div class="mt-6 sm:flex sm:justify-between">
                      <div class="flex items-center">
                        <InformationCircleIcon class="h-5 w-5 text-green-500" aria-hidden="true" />
                        <p class="ml-2 text-sm font-medium text-gray-500">
                          Delivered on <time :datetime="order.orderDate">{{ getLocalTime(order.orderDate) }}</time>
                        </p>
                      </div>
  
                      <div class="mt-6 flex items-center space-x-4 divide-x divide-gray-200 border-t border-gray-200 pt-4 text-sm font-medium sm:ml-4 sm:mt-0 sm:border-none sm:pt-0">
                        <div class="flex flex-1 justify-center">
                          <a  class="whitespace-nowrap text-blue-500 hover:text-blue-400">View shopping list</a>
                        </div>
                        <div class="flex flex-1 justify-center pl-4">
                          <a href="/shopping-lists" class="whitespace-nowrap text-blue-500 hover:text-blue-400">Order again</a>
                        </div>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </template>
  
  <script setup>
  import {
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    Popover,
    PopoverButton,
    PopoverGroup,
    PopoverPanel,
  } from '@headlessui/vue'
  import { EllipsisVerticalIcon, MagnifyingGlassIcon, ShoppingBagIcon } from '@heroicons/vue/24/outline'
  import { CheckCircleIcon, ExclamationCircleIcon, InformationCircleIcon } from '@heroicons/vue/20/solid'
  
  const props = defineProps({
      orders: Array
  });

  function getLocalTime(date) {
    if (!date) return '';

    const parsedDate = new Date(date);
    return parsedDate.toLocaleDateString(undefined, {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
  }
  </script>