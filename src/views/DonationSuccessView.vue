<template>
  <div class="min-h-screen py-12 bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom">
      <div class="max-w-2xl mx-auto text-center">
        <div class="card bg-white p-10 rounded-2xl shadow-lg">
          <div class="text-6xl mb-6 text-green-500 animate-bounce">✅</div>
          <h1 class="text-4xl font-bold text-primary-700 mb-4 text-shadow">התרומה התקבלה בהצלחה!</h1>
          <p class="text-xl text-gray-600 mb-8">
            תודה על תרומתך לקמחא דפסחא. בזכותך, משפחות נזקקות יוכלו לחגוג את חג הפסח בכבוד ובשמחה.
          </p>
          
          <!-- פרטי התשלום -->
          <div v-if="transactionId" class="bg-primary-50 p-6 rounded-xl mb-8 border border-primary-100">
            <h2 class="text-xl font-bold text-primary-700 mb-4">פרטי התרומה:</h2>
            <div class="space-y-2 text-right">
              <p class="text-lg text-gray-700">
                <strong>מספר אסמכתא:</strong> <span class="font-medium">{{ transactionId }}</span>
              </p>
              <p class="text-lg text-gray-700">
                <strong>סכום תרומה:</strong> <span class="font-medium">₪{{ formatNumber(amount) }}</span>
              </p>
              <template v-if="paymentType === 'Ragil'">
                <p v-if="payments > 1" class="text-lg text-gray-700">
                  <strong>מספר תשלומים:</strong> <span class="font-medium">{{ payments }}</span>
                </p>
                <p v-if="payments > 1" class="text-lg text-gray-700">
                  <strong>סכום לתשלום:</strong> <span class="font-medium">₪{{ formatNumber(Math.round(amount / payments)) }} × {{ payments }}</span>
                </p>
              </template>
              <template v-else-if="paymentType === 'HK'">
                <p class="text-lg text-gray-700">
                  <strong>סוג תשלום:</strong> <span class="font-medium">הוראת קבע חודשית</span>
                </p>
                <p class="text-lg text-gray-700">
                  <strong>משך הוראת הקבע:</strong> <span class="font-medium">{{ period || 'ללא הגבלה' }}</span>
                </p>
                <p class="text-lg text-gray-700">
                  <strong>סכום חודשי:</strong> <span class="font-medium">₪{{ formatNumber(amount) }}</span>
                </p>
              </template>
            </div>
          </div>
          
          <p class="text-lg text-gray-600 mb-8">
            אישור על התרומה נשלח לכתובת הדוא"ל שלך.
          </p>
          
          <!-- שיתוף ההודעה -->
          <div class="mb-8">
            <ShareButtons 
              title="שתפו את עמוד תרומת קמחא דפסחא" 
              text="תרמתי כעת לקמחא דפסחא של כולל שערי ניסים. הצטרפו גם אתם ועזרו למשפחות נזקקות!"
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
    ShareButtons
  },
  data() {
    return {
      transactionId: '',
      amount: 0,
      paymentType: 'Ragil',
      period: '',
      payments: 1
    }
  },
  mounted() {
    // קבלת פרמטרים מה-URL
    this.transactionId = this.$route.query.transactionId || '';
    this.amount = this.$route.query.amount || 0;
    this.paymentType = this.$route.query.type || 'Ragil';
    this.period = this.$route.query.period || '';
    this.payments = this.$route.query.payments || 1;
  },
  methods: {
    formatNumber(number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
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