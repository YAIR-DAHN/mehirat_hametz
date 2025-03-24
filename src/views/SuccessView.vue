<template>
  <div class="min-h-screen py-12 bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom">
      <div class="max-w-2xl mx-auto text-center">
        <div class="card bg-white p-10 rounded-2xl shadow-lg">
          <div class="text-6xl mb-6 text-green-500 animate-bounce">✅</div>
          <h1 class="text-4xl font-bold text-primary-700 mb-4 text-shadow">הטופס נשלח בהצלחה!</h1>
          <p class="text-xl text-gray-600 mb-8">
            תודה שמילאת את טופס מכירת החמץ. הפרטים נשמרו במערכת.
          </p>
          
          <!-- שיתוף ההודעה -->
          <div class="mb-8">
            <ShareButtons 
              title="שתפו את טופס מכירת החמץ" 
              text="מילאתי את טופס מכירת החמץ של כולל שערי ניסים. גם אתם יכולים למלא בקלות ובמהירות!"
              size="large"
            />
          </div>
          
          <!-- תרומה לקמחא דפסחא -->
          <div class="p-6 bg-primary-50 rounded-xl mb-8 border border-primary-100">
            <h2 class="text-2xl font-bold text-primary-800 mb-2">מעוניינים לתרום לקמחא דפסחא?</h2>
            <p class="text-lg text-gray-600 mb-4">
              בתרומתכם תוכלו לסייע למשפחות נזקקות לחגוג את חג הפסח בכבוד
            </p>
            <router-link to="/kimcha" class="text-xl py-3 px-8 inline-block transform hover:scale-105 transition-transform duration-300 rounded-lg font-bold text-white shadow-lg bg-gradient-to-r from-green-600 to-green-700 hover:from-green-700 hover:to-green-800 border border-green-600">
              לתרומה לקמחא דפסחא
            </router-link>
          </div>
          
          <div class="space-y-4">
            <router-link to="/" class="btn-primary text-xl py-3 px-8 inline-block transform hover:scale-105 transition-transform duration-300">
              חזרה לדף הבית
            </router-link>
            <div class="mt-4">
              <a href="https://63863ecdd7031.site123.me/" target="_blank" class="text-primary-600 hover:text-primary-700 font-medium">
                לאתר הראשי של הארגון
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import LogoHeader from '../components/LogoHeader.vue'
import ShareButtons from '../components/ShareButtons.vue'

export default {
  name: 'SuccessView',
  components: {
    LogoHeader,
    ShareButtons
  }
}
</script>

<style scoped>
.card {
  transition: all 0.3s ease;
}

.text-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.btn-primary {
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  background: linear-gradient(to right, var(--tw-gradient-from), var(--tw-gradient-to));
  --tw-gradient-from: #4f46e5;
  --tw-gradient-to: #6366f1;
  box-shadow: 0 10px 15px -3px rgba(79, 70, 229, 0.2), 0 4px 6px -2px rgba(79, 70, 229, 0.1);
}

.btn-primary:hover {
  box-shadow: 0 20px 25px -5px rgba(79, 70, 229, 0.3), 0 10px 10px -5px rgba(79, 70, 229, 0.2);
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(-25%);
    animation-timing-function: cubic-bezier(0.8, 0, 1, 1);
  }
  50% {
    transform: translateY(0);
    animation-timing-function: cubic-bezier(0, 0, 0.2, 1);
  }
}

.animate-bounce {
  animation: bounce 1s infinite;
}
</style> 