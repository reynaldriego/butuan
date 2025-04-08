<script setup>
  import { ref } from 'vue'

  const theme = ref('light')

  function onClick () {
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
  <v-responsive class="border rounded">
    <v-app :theme="theme">
      <v-app-bar :color="theme === 'light' ? 'grey' : 'blue-grey-lighten-1' " class="text-white">
        <v-spacer title class="font-weight-bold">
          EXPLORA D' EXPLORER
        </v-spacer>
        <v-btn
          :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
           @click="onClick"
           variant="elevated"
        ></v-btn>
      </v-app-bar>

      <v-main>
        <v-container class="d-flex align-center justify-center" style="min-height: 70vh;">
            <slot name="content"> </slot>

        </v-container>
      </v-main>

      <v-footer 
  app 
  class="text-center d-flex flex-column ga-1 py-2" 
  :color="theme === 'light' ? 'grey-darken-4' : 'blue-grey-darken-4'"
>
  <div class="d-flex ga-2">
    <v-btn
      v-for="icon in icons"
      :key="icon"
      :icon="icon"
      density="compact"
      variant="text"
      size="small"
    ></v-btn>
  </div>

  <v-divider class="my-1" thickness="2" width="40"></v-divider>

  <div class="text-white font-weight-regular opacity-60 text-caption mx-4">
    Your gateway to seamless hotel stays and unforgettable travel adventures...
  </div>

  <v-divider class="mt-1"></v-divider>

  <div class="text-caption py-1">
    <strong>Explora D' Explorer</strong>
  </div>
</v-footer>

</v-app>
  </v-responsive>
  </template>