<template>
    <div class="loading-indicator" :style="{ height: height }">
        <div class="spinner"></div>
        <div class="loading-text">{{ Message }}</div>
    </div>
</template>
<script setup>
const props = defineProps ({
    Message: String,
    height: {
        type: String,
        default: '100vh' // Default height
    }
});
</script>
<style scoped>
    .loading-indicator {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
    }

    .spinner {
        border: 4px solid rgba(0, 0, 0, 0.1);
        border-left-color: rgb(49, 166, 255);
        border-radius: 50%;
        width: 50px;
        height: 50px;
        animation: spin 1s linear infinite;
    }

    @keyframes spin {
        to {
            transform: rotate(360deg);
        }
    }

    .loading-text {
        margin-top: 20px;
    }
</style>