<template>
  <div class="min-h-screen py-12 bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom">
      <div class="max-w-2xl mx-auto text-center">
        <div class="card bg-white p-10 rounded-2xl shadow-lg">
          <div class="text-center mb-8">
            <h1 class="text-3xl md:text-4xl font-bold text-green-700 mb-4 animation-slide-up">
              התרומה התקבלה בהצלחה!
            </h1>
            <div class="text-lg text-gray-600 animation-slide-up animation-delay-200">
              <p class="mb-2">תודה על תרומתך הנדיבה לקמחא דפסחא.</p>
              <p>קבלה נשלחה לדואר האלקטרוני שלך.</p>
            </div>
          </div>

          <!-- פרטי התרומה -->
          <div class="bg-white rounded-lg shadow-lg p-6 mb-8 animation-slide-up animation-delay-400">
            <h2 class="text-xl font-bold text-gray-800 mb-4">פרטי התרומה</h2>
            <div class="space-y-4">
              <div class="flex justify-between">
                <span class="text-gray-600">מספר עסקה:</span>
                <span class="font-medium">{{ $route.query.transactionId }}</span>
              </div>
              <div class="flex justify-between">
                <span class="text-gray-600">סכום:</span>
                <span class="font-medium">₪{{ formattedAmount }}</span>
              </div>
              <div v-if="$route.query.type === 'Ragil' && $route.query.payments > 1" class="flex justify-between">
                <span class="text-gray-600">תשלומים:</span>
                <span class="font-medium">{{ $route.query.payments }}</span>
              </div>
              <div v-if="$route.query.type === 'HK'" class="flex justify-between">
                <span class="text-gray-600">משך הוראת הקבע:</span>
                <span class="font-medium">{{ $route.query.period }}</span>
              </div>
            </div>
          </div>

          <!-- כפתורי שיתוף -->
          <div class="bg-white rounded-lg shadow-lg p-6 mb-8 animation-slide-up animation-delay-600">
            <h2 class="text-xl font-bold text-gray-800 mb-4">שתפו את המצווה</h2>
            <p class="text-gray-600 mb-6">שתפו את הזכות עם חברים ומשפחה ותסייעו למשפחות נזקקות</p>
            <ShareButtons 
              title="תרמתי כעת לקמחא דפסחא" 
              text="הצטרפו אלי לתרומה לקמחא דפסחא לפסח - כולל שערי ניסים"
              size="large"
            />
          </div>
          
          <!-- אפשרות להשאיר הודעת ברכה -->
          <div class="p-6 bg-purple-50 rounded-xl mb-8 border border-purple-100">
            <h2 class="text-2xl font-bold text-purple-700 mb-2">רוצים להוסיף ברכה?</h2>
            <p class="text-lg text-gray-600 mb-4">
              השאירו לנו הודעת ברכה אישית, ונפרסם אותה בלוח הברכות באתר
            </p>
            <button class="bg-purple-600 hover:bg-purple-700 text-white font-bold py-3 px-8 rounded-lg transition-transform transform hover:scale-105">
              השאירו ברכה
            </button>
          </div>
          
          <div class="space-y-4">
            <router-link to="/" class="btn-primary text-xl py-3 px-8 inline-block transform hover:scale-105 transition-transform duration-300">
              חזרה לדף הבית
            </router-link>
            <div class="mt-4">
              <router-link to="/kimcha" class="text-primary-600 hover:text-primary-700 font-medium">
                חזרה לעמוד קמחא דפסחא
              </router-link>
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
  name: 'DonationSuccessView',
  components: {
    LogoHeader,
    ShareButtons,
  },
  data() {
    return {
      // הנתונים יגיעו מה-query parameters
    }
  },
  computed: {
    formattedAmount() {
      const amount = parseFloat(this.$route.query.amount) || 0;
      return amount.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
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