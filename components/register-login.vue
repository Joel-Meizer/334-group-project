<template>
<div v-if="isLoading">
    <loading-indicator :Message="message" />
</div>
<div style="margin-top: 200px; margin-bottom: auto">
    <div class="flex min-h-full flex-1 flex-col justify-center px-6 py-12 lg:px-8">
      <div class="sm:mx-auto sm:w-full sm:max-w-sm">
        <img class="mx-auto h-20 w-auto" src="@\StockImages\frideMatewhiteBG.png" alt="Your Company" />
        <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your account</h2>
      </div>
  
      <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
        <form class="space-y-6" action="#" method="POST">
          <div>
            <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
            <div class="mt-2">
              <input v-model="email" id="email" name="email" type="email" autocomplete="email" required="" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
            </div>
          </div>
  
          <div>
            <div class="flex items-center justify-between">
              <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
              <div class="text-sm">
                <a href="#" class="font-semibold text-blue-500 hover:text-blue-600">Forgot password?</a>
              </div>
            </div>
            <div class="mt-2">
              <input v-model="password" id="password" name="password" type="password" autocomplete="current-password" required="" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-blue-500 sm:text-sm sm:leading-6" />
            </div>
          </div>
  
          <div>
            <button @click.prevent="login()" class="flex w-full justify-center rounded-md bg-blue-500 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-blue-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-500">Sign in</button>
          </div>
        </form>
        
        <p class="mt-10 text-center text-sm text-gray-500">
          Not a member?
          {{ ' ' }}
          <a href="#" class="font-semibold leading-6 text-blue-500 hover:text-blue-600"><span><sign-up /></span></a>
        </p>
      </div>
    </div>
</div>
</template>

<script setup>
import { ref } from 'vue';

const email = ref('');
const password = ref('');
const message = ref('Verifying your login credentials...')
const isLoading = ref(false);

async function login() {
  isLoading.value = true
  const url = `https://localhost:7249/api/UserAccount/Validate`
  const response = await useFetch(url, {
    body: { email : email.value, password : password.value},
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
  });

  const result = await response
  if(result.status.value == 'success') {
    message.value = "Success!"
    sessionStorage.setItem("334_group_user_displayName", result.data.value.user.displayName);
    sessionStorage.setItem("334_group_user_userId", result.data.value.user.id);
    window.location.href = "/home-page"
    isLoading.value = false
  } else {
    isLoading.value = false
  }

};






</script>