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

      <v-footer app class="text-center d-flex flex-column ga-2 py-4 font-weight-bold" :color="theme === 'light' ? 'grey-darken-4' : 'blue-grey-darken-4' ">
        <div class="d-flex ga-3">
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
          Your gateway to seamless hotel stays and unforgettable travel adventures. Whether you're planning a luxury getaway or a budget-friendly escape, Explora D'Explorer connects you to the finest accommodations and hidden gems around the world. Book with confidence and explore with ease.
        </div>

        <v-divider></v-divider>

        <div>
          <strong>Explora D' Explorer</strong>
        </div>
      </v-footer>
    </v-app>
  </v-responsive>
</template>