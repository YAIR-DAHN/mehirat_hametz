<template>
  <nav class="bg-white shadow-md sticky top-0 z-40 border-b border-gray-100">
    <div class="container-custom">
      <div class="flex justify-between items-center py-4">
        <router-link to="/" class="font-bold text-xl md:text-2xl text-primary-700 transform hover:scale-105 transition-transform duration-300">
          מכירת חמץ
        </router-link>
        
        <div class="hidden md:flex space-x-4 items-center">
          <router-link to="/" class="nav-link" active-class="nav-link-active">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
            </svg>
            דף הבית
          </router-link>
          <router-link to="/form" class="nav-link" active-class="nav-link-active">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
            מכירת חמץ
          </router-link>
          <router-link to="/kimcha" class="nav-link" active-class="nav-link-active">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            קמחא דפסחא
          </router-link>
          <!-- קישור לאתר הארגון -->
          <a href="https://63863ecdd7031.site123.me/" class="nav-link" target="_blank">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-1 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            אתר הארגון
          </a>
        </div>
        
        <div class="md:hidden">
          <button @click="toggleMenu" class="text-gray-700 hover:text-primary-600 focus:outline-none">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path v-if="!menuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
      
      <!-- Mobile Menu -->
      <div 
        v-if="menuOpen" 
        class="md:hidden py-2 mb-2 border-t border-gray-200"
        :class="{'menu-enter': menuOpen}"
      >
        <router-link to="/" class="mobile-nav-link" @click="menuOpen = false">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
          </svg>
          דף הבית
        </router-link>
        <router-link to="/form" class="mobile-nav-link" @click="menuOpen = false">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
          מכירת חמץ
        </router-link>
        <router-link to="/kimcha" class="mobile-nav-link" @click="menuOpen = false">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          קמחא דפסחא
        </router-link>
        <a href="https://63863ecdd7031.site123.me/" class="mobile-nav-link" target="_blank" @click="menuOpen = false">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 inline-block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          אתר הארגון
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      menuOpen: false
    }
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen
    }
  }
}
</script>

<style scoped>
.nav-link {
  color: #4b5563;
  padding: 0.5rem 1rem;
  margin: 0 0.25rem;
  border-radius: 0.5rem;
  font-weight: 500;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
}

.nav-link:hover {
  color: var(--tw-color-primary-600);
  background-color: rgba(79, 70, 229, 0.05);
  transform: translateY(-2px);
}

.nav-link-active {
  color: var(--tw-color-primary-700);
  font-weight: 600;
  background-color: rgba(79, 70, 229, 0.1);
}

.mobile-nav-link {
  display: flex;
  align-items: center;
  padding: 0.75rem 1rem;
  margin-bottom: 0.25rem;
  color: #4b5563;
  font-weight: 500;
  transition: all 0.2s ease;
}

.mobile-nav-link:hover {
  background-color: rgba(79, 70, 229, 0.05);
  color: var(--tw-color-primary-600);
}

.menu-enter {
  animation: slideDown 0.3s ease-out forwards;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style> 