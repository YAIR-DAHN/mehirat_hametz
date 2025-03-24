<script>
import Navbar from './components/Navbar.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    AppFooter
  }
}
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <Navbar />
    <main class="flex-grow">
      <router-view />
    </main>
    <AppFooter />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Heebo:wght@400;500;700&display=swap');

html {
  direction: rtl;
  font-family: 'Heebo', system-ui, sans-serif;
}

.container-custom {
  @apply max-w-7xl mx-auto px-4 sm:px-6 lg:px-8;
}

.card {
  @apply bg-white p-6 rounded-lg shadow-sm;
}

.btn-primary {
  @apply bg-primary-600 text-white rounded-lg hover:bg-primary-700 transition-colors duration-200;
}

.form-label {
  @apply block text-gray-700 text-lg mb-2;
}

.form-input {
  @apply w-full rounded-lg border-gray-300 shadow-sm focus:border-primary-500 focus:ring-1 focus:ring-primary-500;
}
</style>
