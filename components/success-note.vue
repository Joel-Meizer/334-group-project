<template>
    <div aria-live="assertive" class="pointer-events-none fixed inset-0 flex items-end px-4 py-6 sm:items-start sm:p-6">
      <div class="flex w-full flex-col items-center space-y-4 sm:items-end">
        <!-- Notification panel, dynamically insert this into the live region when it needs to be displayed -->
        <transition>
          <div :class="{ 'successNote': !show, 'hideRight': show }" class="successNote pointer-events-auto w-full max-w-sm overflow-hidden rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5 relative">
            <div class="p-4">
              <div class="flex items-start">
                <div class="flex-shrink-0">
                  <CheckCircleIcon class="h-6 w-6 text-green-400" aria-hidden="true" />
                </div>
                <div class="ml-3 w-0 flex-1 pt-0.5">
                  <p class="text-sm font-medium text-gray-900">Successfully created your account, go ahead and log in.</p>
                </div>
              </div>
              <div class="progress-bar" :style="{ width: progress + '%' }"></div>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </template>
  
  <script setup>
  import { CheckCircleIcon } from '@heroicons/vue/24/outline'
  import { defineProps, ref, watchEffect } from 'vue'
  
  const props = defineProps({
    show: Boolean
  });
  
  const progress = ref(100);
  
  watchEffect(() => {
    if (props.show) {
      progress.value = 100;
      const updateProgress = () => {
        progress.value -= 1;
        if (progress.value > 0) {
          setTimeout(updateProgress, 100);
        }
      };
      updateProgress();
    }
  });
  </script>
  
  <style>
  .successNote {
    margin-right: -500px;
    transition: ease-in-out 0.5s all;
  }
  
  .hideRight {
    margin-right: 0;
    transition: ease-in-out 0.5s all;
  }
  
  .progress-bar {
    height: 4px;
    background-color: #4CAF50; /* Green */
    position: absolute;
    bottom: 0;
    left: 0;
  }
  </style>
  