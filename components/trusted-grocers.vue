<template>
  <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 mt-8">
    <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      <li v-for="store in stores" :key="store.url" class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow">
        <div class="flex flex-1 flex-col p-8">
          <img class="mx-auto h-32 w-32 flex-shrink-0 rounded-full" :src="store.imageUrl" alt="" />
          <h3 class="mt-6 text-sm font-medium text-gray-900">{{ store.name }}</h3>
          <dl class="mt-1 flex flex-grow flex-col justify-between">
            <dt class="sr-only">Title</dt>
            <dd class="text-sm text-gray-500">{{ store.title }}</dd>
            <dt class="sr-only">Role</dt>
            <dd class="mt-3">
              <span class="inline-flex items-center rounded-full bg-green-50 px-2 py-1 text-xs font-medium text-green-700 ring-1 ring-inset ring-green-600/20">{{ store.role }}</span>
            </dd>
          </dl>
        </div>
        <div>
          <div class="-mt-px flex divide-x divide-gray-200">
            <div class="flex w-0 flex-1">
              <a :href="store.url" target=”_blank” class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
                Navigate to {{store.name}}
              </a>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
  </template>
  <script setup>
  import { EnvelopeIcon, PhoneIcon } from '@heroicons/vue/20/solid'
  
  const stores = [
    {
      name: 'Coles',
      role: 'Trusted Grocer',
      url: 'https://www.coles.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'Woolworths',
      role: 'Trusted Grocer',
      url: 'https://www.woolworths.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'IGA',
      role: 'Trusted Grocer',
      url: 'https://www.iga.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'Foodworks',
      role: 'Trusted Grocer',
      url: 'https://www.foodworks.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'Costco',
      role: 'Trusted Grocer',
      url: 'https://www.costco.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'Drakes',
      role: 'Trusted Grocer',
      url: 'https://drakes.com.au/',
      imageUrl:
        'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60',
    },
    {
      name: 'LiquorLand',
      role: 'Trusted Grocer',
      url: 'https://www.liquorland.com.au/',
      imageUrl:
          "@/StockImages/liquorlandlogo.png",
    },
  ]
  </script>