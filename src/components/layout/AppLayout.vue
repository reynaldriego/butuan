<script setup>
import { ref } from 'vue'

const theme = ref('light')

function onClick() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const icons = [
  'mdi-facebook',
  'mdi-twitter',
  'mdi-linkedin',
  'mdi-instagram',
]
</script>

<template>
  <v-app :theme="theme">
    <!-- Centered App Bar -->
    <v-app-bar 
      :color="theme === 'light' ? 'grey' : 'blue-grey-lighten-1'" 
      class="text-white d-flex justify-center px-6"
      height="60"
      flat
    >
      <v-toolbar-title class="font-weight-bold text-h6">
        EXPLORA D'EXPLORER
      </v-toolbar-title>
      <v-spacer />
      <v-btn
        :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
        @click="onClick"
        variant="text"
        size="small"
        class="ml-2"
      ></v-btn>
    </v-app-bar>

    <!-- Main Content Area -->
    <v-main>
      <v-container class="fill-height d-flex align-center justify-center px-4">
        <v-sheet 
          width="200%"
          max-width="800px"
          class="text-center pa-8"
          color="transparent"
        >
          <slot name="content"></slot>

          <!-- Additional Content -->
          <div class="text-body-1 mb-8 mt-6" style="line-height: 1.7">
            Where extraordinary stays meet unforgettable journeys.<br>
            We uncover the places that turn trips into stories.
          </div>

          <div class="text-caption">
            Explora d' Explorer © {{ new Date().getFullYear() }}
          </div>
        </v-sheet>
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer 
      app 
      class="text-center d-flex flex-column ga-2 py-4 font-weight-bold"
      :color="theme === 'light' ? 'grey-darken-4' : 'blue-grey-darken-4'"
      height="auto"
    >
      <div class="d-flex ga-3 justify-center">
        <v-btn
          v-for="icon in icons"
          :key="icon"
          :icon="icon"
          density="comfortable"
          variant="text"
        ></v-btn>
      </div>

      <v-divider class="my-2" thickness="3" width="50"></v-divider>

      <div class="text-white font-weight-regular opacity-60">
        Your gateway to seamless hotel stays and unforgettable travel adventures.
      </div>

      <v-divider class="mt-1"></v-divider>

      <div class="text-caption">
        <strong>Explora D' Explorer</strong> © {{ new Date().getFullYear() }}
      </div>
    </v-footer>
  </v-app>
</template>