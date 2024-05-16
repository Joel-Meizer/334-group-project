<template>
    <topnav />
    <div class="pl-72">
        <div v-if="isLoading">
            <loading-indicator :Message=message />
        </div>
        <div v-else>
            <header-text headerText="Alerts" subHeaderText="View alerts as they arrive. Including successful orders, to failed orders all the way to new suggestions and updates."/>
            <div v-if="alerts.length > 0" v-for="alert in alerts">
                <div v-if="alert.alertType == 'softwareUpdate'" class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
                    <software-update/>
                </div>
                <div v-if="alert.alertType == 'insufficientFund'" class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
                    <you-broke />
                </div>
                <div v-if="alert.alertType == 'successful'" class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
                    <success :message="alert.alertText"/>
                </div>
                <div v-if="alert.alertType == 'error'" class="mx-auto max-w-7xl sm:px-2 lg:px-8 pt-8">
                    <error />
                </div>
            </div>
            <div v-else style="padding-left: 80px;padding-right: 80px; padding-bottom: 15px;" class="rounded-lg">
            <div class="col-span-full">
            <div class="mt-2 flex justify-center rounded-lg border border-dashed border-gray-900/25 px-6 py-10">
              <div class="text-center">
                <div class="mt-4 flex text-sm leading-6 text-gray-600" style="height:300px; text-align: center; line-height: 300px;">
                  <label class="relative cursor-pointer rounded-md bg-white font-semibold text-blue-400 focus-within:outline-none focus-within:ring-2 focus-within:ring-indigo-600 focus-within:ring-offset-2">
                    <p>You have no new alerts. Come back later and you might see something...</p>
                  </label>
                </div>
              </div>
            </div>
          </div>
          </div>
        </div>
        <padding-item />
        <footer-file />
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const message = ref("Collecting your alerts...")
const isLoading = ref(true)
const alerts = ref([])

async function getUserAlerts() {
    try {
        const response = await fetch('https://localhost:7249/api/UserAccount/Get/6645e7b34a5f82fec3f4b448')
        const data = await response.json();
        alerts.value = data.alerts
        isLoading.value = false;  
    } catch (error) {
        isLoading.value = false
    }
}

onMounted(getUserAlerts)
</script>