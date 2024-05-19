<template>
    <div class="divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow">
      <div class="px-4 py-5 sm:p-6">
        <div class="mx-auto max-w-7xl sm:px-2 lg:px-8">
            <textarea v-model="inputMessage" rows="3" class="px-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
        </div>
      </div>
      <button type="submit" style="min-width: 120px; margin-left: 120px;" @click.prevent="getAIResponse()" class="mb-5 rounded-md bg-blue-400 mr-10 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-600 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Generate Response</button>
      <div class="px-4 py-4 sm:px-6">
        <div class="mx-auto max-w-7xl sm:px-2 lg:px-8">
            <div>Output:</div>
        </div>
      </div>
      <div class="px-4 py-4 sm:px-6">
        <div v-if="isLoading">
              <loading-indicator :Message=message :height="'20vh'" />
          </div>
        <div v-else class="mx-auto max-w-7xl sm:px-2 lg:px-8">
            <div >
                <textarea v-model="outputMessage" rows="16" disabled class="px-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
            </div>
        </div>
      </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const inputMessage = ref("")
const outputMessage = ref("")
const message = ref("Generating you a response...")
const isLoading = ref(false)

async function getAIResponse() {
  outputMessage.value = ""
  isLoading.value = true
  const inputMessageAI = inputMessage.value;
  const encodedMessage = encodeURIComponent(inputMessageAI);
  const url = `https://localhost:7249/api/AI/GetAISpeech?message=${encodedMessage}`;
    const response = await fetch(url, {
        headers: {
          "content-type": "application/json"
        },
        method: 'POST'
    });

    const responseText = await response.json()

    outputMessage.value = responseText.choices[0].message.content
    isLoading.value = false
}
</script>