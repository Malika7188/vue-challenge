<script setup lang="ts">
import { ref, computed } from 'vue';

// Reactive references to store username and password input values
// These automatically update when the user types in the form fields
const username = ref('');
const password = ref('');

// Reactive state management for error handling and form submission status
// apiError: Stores error messages returned from the API to display to users
// isSubmitting: Tracks whether a submission is in progress to prevent duplicate requests
// showValidationErrors: Shows validation errors when user tries to submit invalid form
const apiError = ref('');
const isSubmitting = ref(false);
const showValidationErrors = ref(false);

// Event emitter to communicate with the parent component (app.vue)
// Emits 'create-successful' event when user account is successfully created
const emit = defineEmits(['create-successful']);

// Computed property that dynamically validates password against all requirements
// Returns an array of error messages for validation rules that are not met
const validationCriteria = computed(() => {
  const criteria: string[] = [];

  if (password.value.length < 10) {
    criteria.push('Password must be at least 10 characters long');
  }

  if (password.value.length > 24) {
    criteria.push('Password must be at most 24 characters long');
  }

  if (password.value.includes(' ')) {
    criteria.push('Password cannot contain spaces');
  }

  if (!/\d/.test(password.value)) {
    criteria.push('Password must contain at least one number');
  }

  if (!/[A-Z]/.test(password.value)) {
    criteria.push('Password must contain at least one uppercase letter');
  }

  