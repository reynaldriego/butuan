<script setup>
import { ref } from 'vue'
import AppLayout from '@/components/layout/AppLayout.vue'
import { useDisplay } from 'vuetify'
import { supabase } from '@/utils/supabase.js'
import AlertNotification from '@/components/common/AlertNotification.vue'

const { mobile } = useDisplay()

// Add this single line with your other refs
const refVForm = ref(null)

// Unified form data structure (your original code remains unchanged)
const formData = ref({
  firstname: '',
  lastname: '',
  email: '',
  password: '',
  passwordconfirmation: '',
  showPassword: false,
  showConfirmPassword: false,
})

const formAction = ref({
  formProcess: false,
  formErrorMessage: '',
  formSuccessMessage: '',
  formStatus: null,
})

// Validation rules (your original code remains unchanged)
const rules = {
  required: (value) => !!value || 'Field is required',
  min: (v) => !v || v.length >= 8 || 'Min 8 characters',
  email: (v) => !v || /.+@.+\..+/.test(v) || 'E-mail must be valid',
  passwordMatch: () =>
    formData.value.password === formData.value.passwordconfirmation || 'Passwords must match',
}

const touched = ref({
  firstname: false,
  lastname: false,
  email: false,
  password: false,
  passwordconfirmation: false,
})

const formSubmitted = ref(false)

const onBlur = (field) => {
  touched.value[field] = true
}

const getErrorMessages = (field, value, additionalRules = []) => {
  const activeRules = [rules.required, ...additionalRules]
  const shouldValidate = touched.value[field] || formSubmitted.value

  return shouldValidate
    ? activeRules.map((rule) => rule(value)).filter((msg) => typeof msg === 'string')
    : []
}

const handleSubmit = async () => {
  formSubmitted.value = true
  formAction.value.formProcess = true
  formAction.value.formErrorMessage = ''
  formAction.value.formSuccessMessage = ''

  // Validate all fields before submission (your original code remains unchanged)
  if (
    !formData.value.firstname ||
    !formData.value.lastname ||
    !formData.value.email ||
    !formData.value.password ||
    formData.value.password !== formData.value.passwordconfirmation
  ) {
    formAction.value.formErrorMessage = 'Please fill all fields correctly'
    formAction.value.formProcess = false
    return
  }

  try {
    const { data, error } = await supabase.auth.signUp({
      email: formData.value.email,
      password: formData.value.password,
      options: {
        data: {
          first_name: formData.value.firstname,
          last_name: formData.value.lastname,
        },
      },
    })

    if (error) throw error

    console.log('Registration success:', data)
    formAction.value.formSuccessMessage =
      'Registration successful! Please check your email to verify your account.'
    
    // Add these reset lines only (new code):
    refVForm.value?.reset()
    formData.value = {
      firstname: '',
      lastname: '',
      email: '',
      password: '',
      passwordconfirmation: '',
      showPassword: false,
      showConfirmPassword: false,
    }
    Object.keys(touched.value).forEach(key => {
      touched.value[key] = false
    })
    formSubmitted.value = false
    
  } catch (error) {
    console.error('Registration error:', error)
    formAction.value.formErrorMessage = error.message || 'Registration failed'
    formAction.value.formStatus = error.status
  } finally {
    formAction.value.formProcess = false
  }
}
</script>

<template>
  <AppLayout>
    <template #content>
      <AlertNotification
        :form-success-message="formAction.formSuccessMessage"
        :form-error-message="formAction.formErrorMessage"
      ></AlertNotification>

      <v-row justify="center">
        <v-col cols="12" md="6" class="d-flex justify-center">
          <v-card class="mx-auto" width="450" elevation="24">
            <v-card-text class="bg-surface-light pt-6 pb-6 px-6">
              <!-- Add ref to existing v-form (only change in template) -->
              <v-form ref="refVForm" fast-fail @submit.prevent="handleSubmit">
                <v-text-field
                  v-model="formData.firstname"
                  variant="outlined"
                  label="First Name"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('firstname', formData.firstname)"
                  @blur="onBlur('firstname')"
                ></v-text-field>

                <v-text-field
                  v-model="formData.lastname"
                  variant="outlined"
                  label="Last Name"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('lastname', formData.lastname)"
                  @blur="onBlur('lastname')"
                ></v-text-field>

                <v-text-field
                  v-model="formData.email"
                  variant="outlined"
                  label="Email"
                  class="mb-4"
                  color="indigo-darken-2"
                  density="comfortable"
                  :error-messages="getErrorMessages('email', formData.email, [rules.email])"
                  @blur="onBlur('email')"
                ></v-text-field>

                <v-text-field
                  v-model="formData.password"
                  variant="outlined"
                  label="Password"
                  :type="formData.showPassword ? 'text' : 'password'"
                  :append-inner-icon="formData.showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  class="mb-4"
                  density="comfortable"
                  :error-messages="getErrorMessages('password', formData.password, [rules.min])"
                  hint="At least 8 characters"
                  counter
                  @click:append-inner="formData.showPassword = !formData.showPassword"
                  @blur="onBlur('password')"
                ></v-text-field>

                <v-text-field
                  v-model="formData.passwordconfirmation"
                  variant="outlined"
                  label="Password Confirmation"
                  :type="formData.showConfirmPassword ? 'text' : 'password'"
                  :append-inner-icon="formData.showConfirmPassword ? 'mdi-eye-off' : 'mdi-eye'"
                  class="mb-4"
                  density="comfortable"
                  :error-messages="
                    getErrorMessages('passwordconfirmation', formData.passwordconfirmation, [
                      rules.passwordMatch,
                    ])
                  "
                  @click:append-inner="formData.showConfirmPassword = !formData.showConfirmPassword"
                  @blur="onBlur('passwordconfirmation')"
                ></v-text-field>

                <v-btn
                  class="mt-2"
                  color="indigo-darken-2"
                  type="submit"
                  block
                  size="large"
                  prepend-icon="mdi-account-plus"
                  :disabled="formAction.formProcess"
                  :loading="formAction.formProcess"
                >
                  Register
                </v-btn>
              </v-form>

              <v-divider class="my-5"></v-divider>
              <h5 class="text-center">
                Already have account?
                <RouterLink class="text-primary" to="/">Click here to Login</RouterLink>
              </h5>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </template>
  </AppLayout>
</template>