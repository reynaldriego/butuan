<script setup>
  import AppLayout from '@/components/layout/AppLayout.vue';
  import { useDisplay } from 'vuetify'

  const { mobile } = useDisplay()
</script>

<template>
  <AppLayout>
      <template #content>
    

        <v-row justify="center">
            <v-col cols="12" md="6" class="d-flex justify-center">
              <v-card
  class="mx-auto"
  width="450"
  elevation="24"
>
<v-card-title class="text-center"> 
     <v-img class="mx-auto" src="/images/logo.png" :width="mobile ? '75%' : '25%' "></v-img>
    <h3 class="font-weight-black text-center"  >Welcome to Explora</h3>
  </v-card-title>


  <v-card-text class="bg-surface-light pt-6 pb-6 px-6">
    <v-form fast-fail @submit.prevent>
      <v-text-field
        v-model="email"
        variant="outlined"
        prepend-inner-icon="mdi-email"
        label="Email"
        class="mb-4"
        color="indigo-darken-2"
        density="comfortable"
      ></v-text-field>

      <v-text-field
        v-model="password"
        variant="outlined"
        prepend-inner-icon="mdi-lock"
        label="Password"
        type="password"
        class="mb-4"
        density="comfortable"
      ></v-text-field>

      <v-btn class="mt-2" color="indigo-darken-2" type="submit" block size="large" prepend-icon="mdi-login">Login</v-btn>
    </v-form>

    <v-divider class="my-5"></v-divider>

    <h5 class="text-center">Don't have account?
       <RouterLink class="text-primary" to="/register">Click here to Register</RouterLink>
   </h5>

  </v-card-text>
</v-card>
            </v-col>
          </v-row>



      </template>

  </AppLayout>
        
</template>