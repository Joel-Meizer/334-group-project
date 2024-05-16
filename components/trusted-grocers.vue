<template>
  
  <div class="mx-auto max-w-7xl sm:px-2 lg:px-8 mt-8">
    <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      <li v-for="store in stores" :key="store.url" class="col-span-1 flex flex-col divide-y divide-gray-200 rounded-lg bg-white text-center shadow">
        <div class="flex flex-1 flex-col p-8">
          <h3 class="mt-6 text-sm font-medium text-gray-900">{{ store.name }}</h3>
          <dl class="mt-1 flex flex-grow flex-col justify-between">
            <dt class="sr-only">Title</dt>
            <dd class="text-sm text-gray-500">{{ store.title }}</dd>
            <dt class="sr-only">Role</dt>
            <dd class="mt-3">
              <span v-if="store.role == 0" class="inline-flex items-center rounded-full bg-green-50 px-2 py-1 text-xs font-medium text-green-700 ring-1 ring-inset ring-green-600/20">Trusted Grocer</span>
            </dd>
          </dl>
        </div>
        <div>
          <div class="-mt-px flex divide-x divide-gray-200">
            <div class="flex w-0 flex-1">
              <a :href="store.storeURL" target=”_blank” class="relative -mr-px inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-bl-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
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
  const props = defineProps({
      stores: Array
  });
  </script>