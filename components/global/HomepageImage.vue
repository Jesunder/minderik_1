<script setup>
import { ref, onMounted } from 'vue';
const settings = ref(null);  // Initialize as null for loading state
const isLoading = ref(true);  // Loading state to show the content only after data is loaded
const hasError = ref(false);  // Error state to show an error message if data loading fails
// Fetch JSON data using native fetch API
onMounted(async () => {
  try {
    const response = await fetch('../_data/homepage.json');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const jsonData = await response.json();
    settings.value = jsonData;
    isLoading.value = false;  // Stop loading when data is fetched
  } catch (error) {
    hasError.value = true;  // If there's an error, show the error message
    console.error('Error loading settings:', error);
  }
});
</script>

<template>
<div>
    
    <div v-if="isLoading" class="flex items-center justify-center h-screen">
      <p>Loading...</p> <!-- Display loading text or spinner while data is being fetched -->
    </div>
    <div v-else-if="hasError" class="flex items-center justify-center h-screen">
      <p>Error loading homepage settings. Please try again later.</p> <!-- Display error message -->
    </div>
    <div v-else
      class="back bg-cover bg-center h-full"
      :style="{ backgroundImage: settings.thumbnail ? `url(${settings.thumbnail})` : '' }"
    >
    <div class="pr-5">
      <Drawer />
      
    <div class="flex justify-center p-4 ">
      <img src="/public/img/Logo.png" alt="Logo" class="w-[250px] animate-fade animate-duration-[2000ms] animate-delay-[1500ms]" style="position: absolute; left: 30px; bottom: 30px;">
    </div>

    <!--<div class="flex justify-center p-4 ">
      <img src="/public/img/coolback.png" alt="Logo" class="w-[700px]" style="position: absolute; left: 0px; top: 200px;">
    </div> -->

    

    </div>
      <!-- Info section that triggers the hover effect -->
      <div class="info flex flex-col items-center justify-center h-screen">
        <div class="text-left p-1 lg:p-1" style="margin-left: auto; width: 900px; height: 500px;">
          <div class="opacity-80 animate-fade-left animate-once animate-duration-[2000ms] animate-delay-[350ms] p-10 lg:p-20 bg-neutral-200 dark:bg-black bg-opacity-0 dark:bg-opacity-80 rounded-md ">
            <div class="text-xl font-bold">{{ settings.homepage_title }}</div>
            <div class="text-sm opacity-80">{{ settings.body }}</div>

            <div class="flex mt-10">
                <NuxtLink to="https://github.com/Jesunder/minderik_1" target="_blank">
                    <div class="flex-col hidden">
                      <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 256 256">
                          <path fill="currentColor" d="M203.94 76.16A55.73 55.73 0 0 0 199.46 30a4 4 0 0 0-3.46-2a55.78 55.78 0 0 0-46 24h-28a55.78 55.78 0 0 0-46-24a4 4 0 0 0-3.46 2a55.73 55.73 0 0 0-4.48 46.16A53.8 53.8 0 0 0 60 104v8a52.06 52.06 0 0 0 52 52h1.41A36 36 0 0 0 100 192v12H72a28 28 0 0 1-28-28a36 36 0 0 0-36-36a4 4 0 0 0 0 8a28 28 0 0 1 28 28a36 36 0 0 0 36 36h28v20a4 4 0 0 0 8 0v-40a28 28 0 0 1 56 0v40a4 4 0 0 0 8 0v-40a36 36 0 0 0-13.41-28H160a52.06 52.06 0 0 0 52-52v-8a53.8 53.8 0 0 0-8.06-27.84M204 112a44.05 44.05 0 0 1-44 44h-48a44.05 44.05 0 0 1-44-44v-8a45.76 45.76 0 0 1 7.71-24.89a4 4 0 0 0 .53-3.84a47.82 47.82 0 0 1 2.1-39.21a47.8 47.8 0 0 1 38.12 22.1a4 4 0 0 0 3.37 1.84h32.34a4 4 0 0 0 3.37-1.84a47.8 47.8 0 0 1 38.12-22.1a47.82 47.82 0 0 1 2.1 39.21a4 4 0 0 0 .53 3.83A45.85 45.85 0 0 1 204 104Z"></path>
                      </svg>
                    </div>
                    <div class="flex-col">
                    <span class="text-xs opacity-80">My Github Repository</span>
                    </div>
                  </NuxtLink>
            </div>
          </div>
        </div>
      </div>
  </div>
</div>
</template>