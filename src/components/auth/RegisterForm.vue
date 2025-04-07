<template>

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
</template>