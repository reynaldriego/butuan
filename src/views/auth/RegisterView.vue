<script setup>
import { ref } from 'vue';
import AppLayout from '@/components/layout/AppLayout.vue';
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()

// Form fields (unchanged)
const firstname = ref('');
const lastname = ref('');
const email = ref('');
const password = ref('');
const passwordconfirmation = ref('');
const showPassword = ref(false);
const showConfirmPassword = ref(false);

// Added this new ref to track submission
const formSubmitted = ref(false);

// Validation rules (unchanged)
const rules = {
  required: value => !!value || 'Field is required',
  min: v => !v || v.length >= 8 || 'Min 8 characters',
  email: v => !v || /.+@.+\..+/.test(v) || 'E-mail must be valid',
  passwordMatch: () => !passwordconfirmation.value || 
                     (password.value === passwordconfirmation.value) || 
                     'Passwords must match',
};

// Track if fields have been touched (unchanged)
const touched = ref({
  firstname: false,
  lastname: false,
  email: false,
  password: false,
  passwordconfirmation: false
});

// Modified blur handler to also check if form was submitted
const onBlur = (field) => {
  touched.value[field] = true;
};

// New function to handle submission
const handleSubmit = () => {
  formSubmitted.value = true;
  // Your actual submission logic would go here
};

// New computed error messages that respond to typing after submission
const getErrorMessages = (field, value, additionalRules = []) => {
  const activeRules = [rules.required, ...additionalRules];
  const shouldValidate = touched.value[field] || formSubmitted.value;
  
  return shouldValidate 
    ? activeRules.map(rule => rule(value)).filter(msg => typeof msg === 'string')
    : [];
};
</script>

<template>
  <AppLayout>
    <template #content>
      <v-row justify="center">
        <v-col cols="12" md="6" class="d-flex justify-center">
          <v-card class="mx-auto" width="450" elevation="24">
            <!-- All your original template content remains exactly the same until the form -->
            <v-card-text class="bg-surface-light pt-6 pb-6 px-6">
              <v-form fast-fail @submit.prevent="handleSubmit">
                <!-- Updated fields with new error handling -->
                <v-text-field
                  v-model="firstname"
                  variant="outlined"
                  label="First Name"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('firstname', firstname)"
                  @blur="onBlur('firstname')"
                ></v-text-field>

                <v-text-field
                  v-model="lastname"
                  variant="outlined"
                  label="Last Name"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('lastname', lastname)"
                  @blur="onBlur('lastname')"
                ></v-text-field>

                <v-text-field
                  v-model="email"
                  variant="outlined"
                  label="Email"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('email', email, [rules.email])"
                  @blur="onBlur('email')"
                ></v-text-field>

                <v-text-field
                  v-model="password"
                  variant="outlined"
                  label="Password"
                  :type="showPassword ? 'text' : 'password'"
                  :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  class="mb-4"
                  density="comfortable"
                  :error-messages="getErrorMessages('password', password, [rules.min])"
                  hint="At least 8 characters"
                  counter
                  @click:append-inner="showPassword = !showPassword"
                  @blur="onBlur('password')"
                ></v-text-field>

                <v-text-field
                  v-model="passwordconfirmation"
                  variant="outlined"
                  label="Password Confirmation"
                  :type="showConfirmPassword ? 'text' : 'password'"
                  :append-inner-icon="showConfirmPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  class="mb-4"
                  density="comfortable"
                  :error-messages="getErrorMessages('passwordconfirmation', passwordconfirmation, [rules.passwordMatch])"
                  @click:append-inner="showConfirmPassword = !showConfirmPassword"
                  @blur="onBlur('passwordconfirmation')"
                ></v-text-field>

                <!-- Submit button remains unchanged -->
                <v-btn 
                  class="mt-2" 
                  color="indigo-darken-2" 
                  type="submit" 
                  block 
                  size="large"  
                  prepend-icon="mdi-account-plus"
                >
                  Register
                </v-btn>
              </v-form>

              <!-- Rest of your template remains completely unchanged -->
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