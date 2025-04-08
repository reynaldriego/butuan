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
  <v-card-title> 
    <v-img class="mx-auto" src="/images/logo.png" :width="mobile ? '75%' : '25%' "></v-img>
    <h3 class="font-weight-black text-center">Create an Account</h3>
  </v-card-title>

  <v-card-text class="bg-surface-light pt-6 pb-6 px-6">

    <v-form fast-fail @submit.prevent>

<v-text-field
  v-model="firstname"
  variant="outlined"
  label="First Name"
  class="mb-4"
  color="indigo-darken-2"
  density="comfortable"
></v-text-field>

<v-text-field
  v-model="lastname"
  variant="outlined"
  label="Last Name"
  class="mb-4"
  color="indigo-darken-2"
  density="comfortable"
></v-text-field>

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

<v-text-field
  v-model="passwordconfirmation"
  variant="outlined"
  label="Password Confirmation"
  type="password"
  class="mb-4"
  density="comfortable"
></v-text-field>

<v-btn class="mt-2" color="indigo-darken-2" type="submit" block size="large"  prepend-icon="mdi-account-plus">Register</v-btn>
</v-form>

      
    
    <v-divider class="my-5"></v-divider>


    <h5 class="text-center">Already have account? 
        <RouterLink class="text-primary" to="/">Click here to Login</RouterLink>
    </h5>

  </v-card-text>
</v-card>
            </v-col>
          </v-row>

         </template>

         
          
    </AppLayout>
</template>