<script setup lang="ts">
import { ref, computed } from 'vue';

// Reactive references to store username and password input values
// These automatically update when the user types in the form fields
const username = ref('');
const password = ref('');
