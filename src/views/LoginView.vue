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
      <v-app-bar color="indigo-darken-2" class="text-white">
        <v-spacer title class="font-weight-bold">
          EXPLORA D' EXPLORER
        </v-spacer>
        <v-btn
          :icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
           @click="onClick"
           variant="text"
        ></v-btn>
      </v-app-bar>

      <v-main>
        <v-container class="d-flex align-center justify-center" style="min-height: 70vh;">
          <v-row justify="center">
            <v-col cols="12" md="6" class="d-flex justify-center">
              <v-card
  class="mx-auto"
  width="450"
  elevation="24"
  prepend-icon="mdi-account"
  subtitle=" The #1 Travel Booking Platform"
  subtitle-class="text-h6"
>
  <template v-slot:title>
    <span class="font-weight-black text-h4">Welcome to Explora</span>
  </template>

  <v-card-text class="bg-surface-light pt-6 pb-6 px-6">
    <v-form fast-fail @submit.prevent>
      <v-text-field
        v-model="email"
        variant="outlined"
        label="Email"
        class="mb-4"
        color="indigo-darken-2"
        density="comfortable"
      ></v-text-field>

      <v-text-field
        v-model="password"
        variant="outlined"
        label="Password"
        type="password"
        class="mb-4"
        density="comfortable"
      ></v-text-field>

      <v-btn class="mt-2" type="submit" block size="large">Login</v-btn>
    </v-form>

    <v-divider class="my-5"></v-divider>

    <h5 class="text-center">Don't have account?
       <RouterLink class="text-primary" to="/register">Click here to Register</RouterLink>
   </h5>

  </v-card-text>
</v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main>

      <v-footer app class="text-center d-flex flex-column ga-2 py-4" color="indigo-darken-2">
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