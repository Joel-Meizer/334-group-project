<template>
<button  @click.prevent="updateCreationModal">Create a free account today</button>
<div v-if="productForm">
</div>
<div v-else class="relative z-10" role="dialog" aria-modal="true">
    <div class="fixed inset-0 hidden bg-gray-500 bg-opacity-75 transition-opacity md:block hoverNo"></div>
    <div class="fixed inset-0 z-10 w-screen ">
      <div class="flex min-h-full items-stretch justify-center text-center md:items-center md:px-2 lg:px-4 md:mt-10">
        <div class="flex transform text-left text-base transition md:my-8 md:max-w-2xl md:px-4 lg:max-w-4xl">
          <div class="relative flex w-full items-center overflow-hidden bg-white shadow-2xl" style="max-height: 750px;">
            <button @click.prevent="hideCreationModal" type="button" class="absolute right-4 top-4 text-gray-400 hover:text-gray-500 sm:right-6 sm:top-8 md:right-6 md:top-6 lg:right-8 lg:top-8">
              <span class="sr-only">Close</span>
              <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
            <div class="flex w-full justify-center" >
                <div class="bg-white shadow-lg p-7 sm:p-10">
                <h3 class="text-black mb-4 text-xl font-semibold sm:text-center sm:mb-6 sm:text-2xl">
                    Register now to start your site
                </h3>
                <form class="">
                    <div class="mb-1 sm:mb-2">
                    <label for="firstName" class="inline-block mb-1 font-medium text-gray-500">First name</label>
                    <input
                        v-model="firstName"
                        type="text"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6"
                        id="firstName"
                        name="firstName"
                        required
                    />
                    </div>
                    <div class="mb-1 sm:mb-2">
                    <label for="lastName" class="inline-block mb-1 font-medium text-gray-500">Last name</label>
                    <input
                        v-model="lastName"
                        type="text"
                        class="flex-grow w-full h-12 px-4 mb-2 transition duration-200 bg-white border border-gray-300 rounded shadow-sm appearance-none focus:border-blue-500 focus:outline-none focus:shadow-outline"
                        id="lastName"
                        name="lastName"
                        required
                    />
                    </div>
                    <div class="mb-1 sm:mb-2">
                    <label for="email" class="inline-block mb-1 font-medium text-gray-500">E-mail</label>
                    <input
                        v-model="email"
                        type="text"
                        class="flex-grow w-full h-12 px-4 mb-2 transition duration-200 bg-white border border-gray-300 rounded shadow-sm appearance-none focus:border-blue-500 focus:outline-none focus:shadow-outline"
                        id="email"
                        name="email"
                        required
                    />
                    </div>
                    <div class="mb-1 sm:mb-2">
                    <label for="password" class="inline-block mb-1 font-medium text-gray-500">Password</label>
                    <input
                        v-model="password"
                        type="password"
                        class="flex-grow w-full h-12 px-4 mb-2 transition duration-200 bg-white border border-gray-300 rounded shadow-sm appearance-none focus:border-blue-500 focus:outline-none focus:shadow-outline"
                        id="password"
                        name="password"
                        required
                    />
                    </div>
                    <div class="mt-4 mb-2 sm:mb-4">
                    <input
                        @click.prevent="registerUser"
                        type="submit"
                        class="inline-flex items-center justify-center w-full h-12 px-6 font-medium tracking-wide text-white transition duration-200 rounded shadow-md bg-blue-500 hover:bg-blue-700 focus:shadow-outline focus:outline-none"
                    >
                    </div>
                    <p class="text-xs text-gray-600 sm:text-sm">
                    We respect your privacy. Unregister at any time.
                    </p>
                </form>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
<div>
  <success-note :show="false" />
</div>
</template>

<script setup>

import {ref,computed } from 'vue'
const firstName = ref('')
const lastName = ref('')
const password = ref('')
const email = ref('')
const openProductCreation = ref('false')

const productForm = computed(() => openProductCreation.value === 'false')
const registerUser = async () => {

const userData = {
    id: "",
    familyId: "",
    givenName: firstName.value,
    surname: lastName.value,
    displayName: firstName.value + " " + lastName.value,
    Email: email.value,
    Password: password.value,
    emailConfirmed: false,
    type: "",
    phoneNumber: "",
    street: "",
    city: "",
    state: "",
    postalCode: "",
    country: "",
    orderIds: [],
    alerts: []
};
try {
    const response = await useFetch('https://localhost:7249/api/UserAccount/Post', {
        method: 'POST',
        body: JSON.stringify(userData),
        headers: {
            'Content-Type': 'application/json',
        },
    });

    if (response.status.value == "success") {
        hideCreationModal()
    }

} catch (error) {
    console.error('Error registering user:', error);
}
};

function updateCreationModal () {
    openProductCreation.value = 'true'
}

function hideCreationModal() {
    openProductCreation.value = 'false'
}

</script>

<style>
 .hoverNo:hover {
    cursor:none;
 }
</style>