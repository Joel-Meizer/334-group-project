<template>
    <div class="px-6 py-6 hoverStyling">
        <div class=" border-gray-200 bg-white py-2 sm:px-6">
            <h1 class="text-base font-semibold leading-6 text-gray-900">{{headerMessage}}</h1>
        </div>
        <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <li v-for="meal in meals" class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white shadow">
            <div class="flex w-full items-center justify-between space-x-6 p-2">
            <img class="h-40 w-50 flex-shrink-0 bg-gray-300 ml-auto mr-auto" :src="meal.imageUrl" alt="" />
            </div>
            <div>
            <div class="-mt-px flex divide-x divide-gray-200">
                <div class="-ml-px flex w-0 flex-1">
                <a class="relative inline-flex w-0 flex-1 items-center justify-center gap-x-3 rounded-br-lg border border-transparent py-4 text-sm font-semibold text-gray-900">
                    <h3 class="truncate text-sm font-medium text-gray-900">{{ meal.name }}</h3>
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
    headerMessage: String,
    meals: Array
  });

  const meals = [
    {
      name: 'Double Sweet Chilli Asian Beef Tacos',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65f98c7809bba91b1c087515-06d1666d.jpeg',
    },
    {
      name: 'Double Spiced Chicken & Brussels Sprout Toss',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65fa22468a80aebcd2ac9465-6c9a8b6d.jpeg',
    },
    {
      name: 'Double Mild North Indian Butter Chicken',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65fa21fe8a80aebcd2ac9464-cbddd9ba.jpeg',
    },
    {
      name: 'Double Sticky Honey BBQ Pork Steaks',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65f98cde7a463d8b127b86e0-65c7b3da.jpeg',
    },
    {
      name: 'Satay Tofu Tacos & Sweet Chilli Mayo',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65f927ef09bba91b1c0874ea-556598b5.jpeg',
    },
    {
      name: 'Haloumi & Caramelised Onion Burger',
      imageUrl:
        'https://img.hellofresh.com/c_fit,f_auto,fl_lossy,h_1100,q_50,w_2600/hellofresh_s3/image/65f98cde7a463d8b127b86e0-65c7b3da.jpeg',
    },
  ]
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