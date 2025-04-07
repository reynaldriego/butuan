<script setup>
  import AppLayout from '@/components/layout/AppLayout.vue';
  import LoginForm from '@/components/auth/RegisterForm.vue';
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

    <v-divider class="my-5"></v-divider>

       <RegisterForm></RegisterForm>
    
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