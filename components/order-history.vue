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
              <div v-for="order in orders" :key="order.number" class="border-b border-t border-gray-200 bg-white shadow-sm sm:rounded-lg sm:border">
                <h3 class="sr-only">
                  Order placed on <time :datetime="order.createdDatetime">{{ order.createdDate }}</time>
                </h3>
  
                <div class="flex items-center border-b border-gray-200 p-4 sm:grid sm:grid-cols-4 sm:gap-x-6 sm:p-6">
                  <dl class="grid flex-1 grid-cols-2 gap-x-6 text-sm sm:col-span-3 sm:grid-cols-3 lg:col-span-2">
                    <div>
                      <dt class="font-medium text-gray-900">Order number</dt>
                      <dd class="mt-1 text-gray-500">{{ order.number }}</dd>
                    </div>
                    <div class="hidden sm:block">
                      <dt class="font-medium text-gray-900">Date placed</dt>
                      <dd class="mt-1 text-gray-500">
                        <time :datetime="order.createdDatetime">{{ order.createdDate }}</time>
                      </dd>
                    </div>
                    <div>
                      <dt class="font-medium text-gray-900">Total amount</dt>
                      <dd class="mt-1 font-medium text-gray-900">{{ order.total }}</dd>
                    </div>
                  </dl>
  
                  <Menu as="div" class="relative flex justify-end lg:hidden">
                    <div class="flex items-center">
                      <MenuButton class="-m-2 flex items-center p-2 text-gray-400 hover:text-gray-500">
                        <span class="sr-only">Options for order {{ order.number }}</span>
                        <EllipsisVerticalIcon class="h-6 w-6" aria-hidden="true" />
                      </MenuButton>
                    </div>
  
                    <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                      <MenuItems class="absolute right-0 z-10 mt-2 w-40 origin-bottom-right rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
                        <div class="py-1">
                          <MenuItem v-slot="{ active }">
                            <a :href="order.href" :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block px-4 py-2 text-sm']">View</a>
                          </MenuItem>
                          <MenuItem v-slot="{ active }">
                            <a :href="order.invoiceHref" :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block px-4 py-2 text-sm']">Invoice</a>
                          </MenuItem>
                        </div>
                      </MenuItems>
                    </transition>
                  </Menu>
  
                  <div class="hidden lg:col-span-2 lg:flex lg:items-center lg:justify-end lg:space-x-4">
                    <a :href="order.href" class="flex items-center justify-center rounded-md border border-gray-300 bg-white px-2.5 py-2 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                      <span>View Order</span>
                      <span class="sr-only">{{ order.number }}</span>
                    </a>
                    <a :href="order.invoiceHref" class="flex items-center justify-center rounded-md border border-gray-300 bg-white px-2.5 py-2 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                      <span>View Invoice</span>
                      <span class="sr-only">for order {{ order.number }}</span>
                    </a>
                  </div>
                </div>
  
                <!-- Products -->
                <h4 class="sr-only">Items</h4>
                <ul role="list" class="divide-y divide-gray-200">
                  <li v-for="product in order.products" :key="product.id" class="p-4 sm:p-6">
                    <div class="flex items-center sm:items-start">
                      <div class="h-20 w-20 flex-shrink-0 overflow-hidden rounded-lg bg-gray-200 sm:h-40 sm:w-40">
                        <component :is="product.imageSrc" class="h-full w-full object-cover object-center text-gray-600" />
                      </div>
                      <div class="ml-6 flex-1 text-sm">
                        <div class="font-medium text-gray-900 sm:flex sm:justify-between">
                          <h5>{{ product.name }}</h5>
                          <p class="mt-2 sm:mt-0">{{ product.price }}</p>
                        </div>
                        <p class="hidden text-gray-500 sm:mt-2 sm:block">{{ product.description }}</p>
                      </div>
                    </div>
  
                    <div class="mt-6 sm:flex sm:justify-between">
                      <div class="flex items-center">
                        <CheckCircleIcon class="h-5 w-5 text-green-500" aria-hidden="true" />
                        <p class="ml-2 text-sm font-medium text-gray-500">
                          Delivered on <time :datetime="order.deliveredDatetime">{{ order.deliveredDate }}</time>
                        </p>
                      </div>
  
                      <div class="mt-6 flex items-center space-x-4 divide-x divide-gray-200 border-t border-gray-200 pt-4 text-sm font-medium sm:ml-4 sm:mt-0 sm:border-none sm:pt-0">
                        <div class="flex flex-1 justify-center">
                          <a :href="product.href" class="whitespace-nowrap text-indigo-600 hover:text-indigo-500">View shopping list</a>
                        </div>
                        <div class="flex flex-1 justify-center pl-4">
                          <a href="#" class="whitespace-nowrap text-indigo-600 hover:text-indigo-500">Order again</a>
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
  import { EllipsisVerticalIcon, MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
  import { CheckCircleIcon, ShoppingBagIcon } from '@heroicons/vue/20/solid'
  
  const orders = [
  {
      number: 'WU88191113',
      href: '?orderId=WU88191113',
      invoiceHref: '#',
      createdDate: 'Jul 22, 2021',
      createdDatetime: '2021-07-06',
      deliveredDate: 'July 23, 2021',
      deliveredDatetime: '2021-07-12',
      total: '$240.00',
      products: [
        {
          id: 1,
          name: 'Shopping list "Weekly Shop"',
          description:
            'Tomatoes, Onions, Bell peppers, Spinach, Chicken breast, Salmon fillets, Tofu, Brown rice, Quinoa, Whole wheat bread, Greek yogurt, Almond milk, Cottage cheese, Apples, Bananas, Berries (strawberries, blueberries, raspberries), Olive oil, Soy sauce, Garlic, Herbs (basil, oregano, parsley), Eggs, Nuts (almonds, walnuts), Avocado, Whole grain pasta',
          href: '#',
          price: '$240.00',
          imageSrc: ShoppingBagIcon,
        },
      ],
    },
    {
      number: 'WU88191112',
      href: '?orderId=WU88191112',
      invoiceHref: '#',
      createdDate: 'Jul 14, 2021',
      createdDatetime: '2021-07-06',
      deliveredDate: 'July 15, 2021',
      deliveredDatetime: '2021-07-12',
      total: '$240.00',
      products: [
        {
          id: 1,
          name: 'Shopping list "Weekly Shop"',
          description:
            'Tomatoes, Onions, Bell peppers, Spinach, Chicken breast, Salmon fillets, Tofu, Brown rice, Quinoa, Whole wheat bread, Greek yogurt, Almond milk, Cottage cheese, Apples, Bananas, Berries (strawberries, blueberries, raspberries), Olive oil, Soy sauce, Garlic, Herbs (basil, oregano, parsley), Eggs, Nuts (almonds, walnuts), Avocado, Whole grain pasta',
          price: '$240.00',
          imageSrc: ShoppingBagIcon,
        },
      ],
    },
    {
      number: 'WU88191111',
      href: '?orderId=WU88191111',
      invoiceHref: '#',
      createdDate: 'Jul 6, 2021',
      createdDatetime: '2021-07-06',
      deliveredDate: 'July 7, 2021',
      deliveredDatetime: '2021-07-12',
      total: '$240.00',
      products: [
        {
          id: 1,
          name: 'Shopping list "Weekly Shop"',
          description:
            'Tomatoes, Onions, Bell peppers, Spinach, Chicken breast, Salmon fillets, Tofu, Brown rice, Quinoa, Whole wheat bread, Greek yogurt, Almond milk, Cottage cheese, Apples, Bananas, Berries (strawberries, blueberries, raspberries), Olive oil, Soy sauce, Garlic, Herbs (basil, oregano, parsley), Eggs, Nuts (almonds, walnuts), Avocado, Whole grain pasta',
          href: '#',
          price: '$240.00',
          imageSrc: ShoppingBagIcon,
        },
      ],
    },
  ]
  </script>