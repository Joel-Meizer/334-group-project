<template>
    <div class="bg-white py-24 sm:py-32">
      <div class="mx-auto max-w-7xl px-6 lg:px-8">
        <div class="mx-auto max-w-2xl lg:text-center">
          <h2 class="text-base font-semibold leading-7 text-blue-500">Plan easier</h2>
          <p class="mt-2 text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">Everything you need to succeed in your meal planning</p>
          <p class="mt-6 text-lg leading-8 text-gray-600">Offering personalized meal planning solutions, utilizing cutting-edge technology to streamline organization and optimize nutrition. Let us simplify your meal planning journey, tailored to your preferences and dietary needs.</p>
        </div>
        <div class="mx-auto mt-16 max-w-2xl sm:mt-20 lg:mt-24 lg:max-w-4xl">
          <dl class="grid max-w-xl grid-cols-1 gap-x-8 gap-y-10 lg:max-w-none lg:grid-cols-2 lg:gap-y-16">
            <div v-for="feature in features" :key="feature.name" class="relative pl-16">
              <dt class="text-base font-semibold leading-7 text-gray-900">
                <div class="absolute left-0 top-0 flex h-10 w-10 items-center justify-center rounded-lg bg-blue-500">
                  <component :is="feature.icon" class="h-6 w-6 text-white" aria-hidden="true" />
                </div>
                {{ feature.name }}
              </dt>
              <dd class="mt-2 text-base leading-7 text-gray-600">{{ feature.description }}</dd>
            </div>
          </dl>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ArrowPathIcon, ShoppingBagIcon, FingerPrintIcon, FaceSmileIcon, CpuChipIcon, QuestionMarkCircleIcon } from '@heroicons/vue/24/outline'
  
  const features = [
    {
      name: 'Built in shopping lists',
      description:
        'Empower your meal planning experience with built-in shopping lists, seamlessly integrated to streamline your grocery shopping. Simplify your shopping routine and stay organized effortlessly with our intuitive tools.',
      icon: ShoppingBagIcon,
    },
    {
      name: 'Suggested meal plans',
      description:
        'Elevate your culinary journey with our curated selection of suggested meal plans, designed to inspire and simplify your cooking experience. Discover new flavors, optimize nutrition, and enjoy hassle-free meal preparation tailored to your preferences.',
      icon: QuestionMarkCircleIcon,
    },
    {
      name: 'AI assisted information',
      description:
        'Experience intelligent nutrition guidance through our AI-assisted calorie and nutritional information, ensuring informed dietary choices tailored to your health goals. Harness the power of data-driven insights to optimize your wellness journey effortlessly.',
      icon: CpuChipIcon,
    },
    {
      name: 'Supplied from the best',
      description:
        "Teaming up with Australia's best grocers, we offer seamless access to quality ingredients, enriching your meal planning with convenience and freshness.",
      icon: FaceSmileIcon,
    },
  ]
  </script>