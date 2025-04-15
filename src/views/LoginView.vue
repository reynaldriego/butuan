<script setup>
import { ref } from 'vue';
import AppLayout from '@/components/layout/AppLayout.vue';
import { useDisplay } from 'vuetify'
import { RouterLink } from 'vue-router';

const { mobile } = useDisplay()

// Form fields
const email = ref('');
const password = ref('');
const showPassword = ref(false);
const submitted = ref(false); // Track if form was submitted

// Validation rules
const rules = {
  required: value => !!value || 'Required.',
  min: v => v.length >= 8 || 'Min 8 characters',
  email: v => /.+@.+\..+/.test(v) || 'E-mail must be valid'
};

// Validate fields (will show errors after submission)
const validate = (field, value) => {
  return submitted.value ? [rules.required(value), field === 'email' ? rules.email(value) : true].filter(msg => msg !== true) : [];
};

const submitForm = () => {
  submitted.value = true;
  if (!email.value || !password.value || password.value.length < 8 || !rules.email(email.value)) {
    return; // Prevent submission if invalid
  }
  // Your login logic here
};
</script>

<template>
  <AppLayout>
    <template #content>
      <v-row justify="center">
        <v-col cols="12" md="6" class="d-flex justify-center">
          <v-card class="mx-auto" width="450" elevation="24">
            <v-card-title class="text-center"> 
              <v-img class="mx-auto" src="/images/logo.png" :width="mobile ? '75%' : '25%'"></v-img>
              <h3 class="font-weight-black text-center">Welcome to Explora</h3>
            </v-card-title>

            <v-card-text class="bg-surface-light pt-6 pb-6 px-6">
              <v-form @submit.prevent="submitForm">
                <v-text-field
                  v-model="email"
                  variant="outlined"
                  prepend-inner-icon="mdi-email"
                  label="Email"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="validate('email', email)"
                ></v-text-field>

                <v-text-field
                  v-model="password"
                  variant="outlined"
                  prepend-inner-icon="mdi-lock"
                  :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  :type="showPassword ? 'text' : 'password'"
                  label="Password"
                  class="mb-4"
                  density="comfortable"
                  :error-messages="validate('password', password)"
                  hint="At least 8 characters"
                  counter
                  @click:append-inner="showPassword = !showPassword"
                ></v-text-field>

                <v-btn 
                  class="mt-2" 
                  color="indigo-darken-2" 
                  type="submit" 
                  block 
                  size="large" 
                  prepend-icon="mdi-login"
                >
                  Login
                </v-btn>
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