<template>
  <div class="min-h-screen bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom py-8 md:py-12">
      <div class="max-w-4xl mx-auto">
        <!-- Hero Section -->
        <div class="text-center mb-12 bg-white p-8 rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <h1 class="text-4xl md:text-5xl font-bold text-primary-700 mb-6 text-shadow">
            קמחא דפסחא
          </h1>
          <p class="text-xl md:text-2xl text-gray-600 mb-8">
            תרמו למצוות קמחא דפסחא וסייעו למשפחות נזקקות לחגוג את חג הפסח בכבוד
          </p>
          
          <!-- כפתורי שיתוף -->
          <div class="py-4">
            <ShareButtons 
              title="עזרו לנו להפיץ את המצווה" 
              text="סייעו למשפחות נזקקות בחג הפסח - קמחא דפסחא של כולל שערי ניסים"
              size="large"
            />
          </div>
        </div>

       

        <!-- הסבר על קמחא דפסחא -->
        <div class="card mb-8 rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <h2 class="text-3xl font-bold text-primary-800 mb-6 text-center">מעלת מצוות קמחא דפסחא</h2>
          <div class="text-lg text-gray-600 space-y-4">
            <p class="leading-relaxed">
              מצוות קמחא דפסחא היא מנהג עתיק שהחל עוד בתקופת התלמוד. על פי מנהג זה, נהגו לחלק קמח לעניים לפני חג הפסח כדי שיוכלו להכין מצות ולחגוג את החג בכבוד.
            </p>
            <p class="leading-relaxed">
              בימינו, המנהג התרחב וכולל איסוף כספים וחלוקת מצרכי מזון, מצות, יין ושאר צרכי החג למשפחות נזקקות, כדי שיוכלו לקיים את מצוות החג ולשמוח בו כראוי.
            </p>
            <p class="leading-relaxed">
              מצווה זו נחשבת למצווה גדולה במיוחד, שכן היא משלבת בתוכה את מצוות הצדקה ומצוות שמחת החג. חכמינו ז"ל אמרו <span class="text-primary-700 font-semibold">"כל המשמח את העניים ביום טוב כאילו הקריב קרבן"</span>.
            </p>
            <div class="bg-primary-50 border-r-4 border-primary-500 p-4 rounded-lg my-6">
              <p class="leading-relaxed font-medium text-primary-900">
                תרומתכם תסייע למשפחות רבות לחגוג את חג הפסח בשמחה ובכבוד, ותזכו למצוות רבות.
              </p>
            </div>
            <div class="flex justify-center">
            <a href="#donation-form" class="btn-primary text-xl" >
                  תרמו עכשיו
                </a></div>
          </div>
        </div>

         <!-- מודעת קמחא דפסחא -->
         <div class="card mb-8 text-center overflow-hidden rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <img src="../assets/images/kimha.webp" alt="קמחא דפסחא" class="max-w-full h-auto mx-auto rounded-lg hover:scale-105 transition-transform duration-700">
        </div>
        <!-- טופס תרומה -->
        <div class="card mb-4" id="donation-form">
        </div>
        <div class="card mb-8" >
          <h2 class="text-3xl font-bold text-gray-800 mb-6 text-center" >תרמו עכשיו לקמחא דפסחא</h2>
          
          <div v-if="!showIframe" class="max-w-lg mx-auto">
            <form @submit.prevent="startDonation" class="space-y-6">
              <div>
                <label class="form-label">שם פרטי <span class="text-red-500">*</span></label>
                <input type="text" v-model="donationData.firstName" class="form-input" required>
              </div>
              <div>
                <label class="form-label">שם משפחה <span class="text-red-500">*</span></label>
                <input type="text" v-model="donationData.lastName" class="form-input" required>
              </div>
              <div>
                <label class="form-label">טלפון <span class="text-red-500">*</span></label>
                <input type="tel" v-model="donationData.phone" class="form-input" required>
              </div>
              <div>
                <label class="form-label">דוא"ל</label>
                <input type="email" v-model="donationData.email" class="form-input">
              </div>
              <div>
                <label class="form-label">עיר</label>
                <input type="text" v-model="donationData.city" class="form-input">
              </div>
              <div>
                <label class="form-label">רחוב</label>
                <input type="text" v-model="donationData.street" class="form-input">
              </div>
              <div>
                <label class="form-label">סכום תרומה <span class="text-red-500">*</span></label>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-3 mb-3">
                  <button 
                    type="button"
                    class="py-3 px-4 border rounded-lg text-lg" 
                    :class="donationData.amount === 600 ? 'bg-primary-100 border-primary-500 font-bold' : 'border-gray-300 hover:border-primary-400'"
                    @click="donationData.amount = 600"
                  >
                    סל מלא - ₪600
                  </button>
                  <button 
                    type="button"
                    class="py-3 px-4 border rounded-lg text-lg" 
                    :class="donationData.amount === 300 ? 'bg-primary-100 border-primary-500 font-bold' : 'border-gray-300 hover:border-primary-400'"
                    @click="donationData.amount = 300"
                  >
                    חצי סל - ₪300
                  </button>
                </div>
                <div class="text-center text-gray-500 mb-3">- או -</div>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-3 mb-3">
                  <button 
                    v-for="amount in [36, 54, 72, 118, 180, 360, 500, 1000]" 
                    :key="amount"
                    type="button"
                    class="py-2 px-3 border rounded-lg transition-all duration-300 transform hover:scale-105" 
                    :class="donationData.amount === amount ? 'bg-primary-100 border-primary-500 shadow-md scale-105' : 'border-gray-300 hover:border-primary-400'"
                    @click="donationData.amount = amount"
                  >
                    ₪{{ amount }}
                  </button>
                </div>
                <div class="mt-4">
                  <label class="form-label">סכום אחר</label>
                  <input 
                    type="number" 
                    v-model.number="donationData.amount" 
                    class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400" 
                    min="1" 
                    placeholder="הזן סכום לתרומה" 
                  >
                </div>
              </div>
              <div>
                <label class="form-label">מספר תשלומים</label>
                <select v-model="donationData.payments" class="form-input">
                  <option value="1">תשלום אחד</option>
                  <option value="2">2 תשלומים</option>
                  <option value="3">3 תשלומים</option>
                  <option value="6">6 תשלומים</option>
                  <option value="12">12 תשלומים</option>
                </select>
              </div>
              <div>
                <label class="form-label">הקדשה (אופציונלי)</label>
                <textarea v-model="donationData.dedication" class="form-input" rows="2" placeholder="לרפואת / לעילוי נשמת"></textarea>
              </div>

              <div class="text-center">
                <button type="submit" class="btn-primary text-xl py-3 px-8">
                  המשך לתשלום
                </button>
                <div class="mt-4">
                  <router-link to="/" class="text-primary-600 hover:text-primary-700">
                    חזרה לדף הבית
                  </router-link>
                </div>
              </div>
            </form>
          </div>

          <div v-else class="iframe-container">
            <iframe 
              v-if="iframeLoaded" 
              ref="nedarimIframe" 
              id="nedarimIframe"
              src="https://www.matara.pro/nedarimplus/iframe/"
              width="100%" 
              :style="{ height: iframeHeight + 'px' }"
              frameborder="0"
            ></iframe>
            <div v-else class="text-center py-8">
              <div class="inline-block animate-spin rounded-full h-8 w-8 border-b-2 border-primary-600"></div>
              <p class="mt-4 text-gray-600">טוען את עמוד התשלום...</p>
            </div>
          </div>
        </div>

        <!-- Call to Action -->
        <div class="text-center p-8 bg-white rounded-2xl shadow-lg" v-if="!showIframe">
          <h2 class="text-3xl font-bold text-primary-700 mb-4">
            כל תרומה חשובה
          </h2>
          <p class="text-xl text-gray-600 mb-6">
            אפילו תרומה קטנה יכולה לעשות הבדל גדול בחייה של משפחה
          </p>
          
          <!-- כפתורי שיתוף -->
          <div class="py-4">
            <ShareButtons 
              title="שתפו עם חברים ומשפחה" 
              text="מצוות קמחא דפסחא - כולל שערי ניסים"
            />
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
  name: 'KimchaView',
  components: {
    LogoHeader,
    ShareButtons
  },
  data() {
    return {
      donationData: {
        firstName: '',
        lastName: '',
        phone: '',
        email: '',
        city: '',
        street: '',
        amount: 180,
        payments: '1',
        dedication: ''
      },
      showIframe: false,
      iframeLoaded: false,
      iframeHeight: 600,
      nedarimConfiguration: {
        Mosad: '7001292',         // מזהה מוסד בנדרים פלוס - צריך להחליף למספר האמיתי
        ApiValid: 'xxxxxxx',      // טקסט אימות - צריך לקבל מהמשרד
        Currency: '1',            // 1 = שקל, 2 = דולר
        PaymentType: 'Ragil',     // סוג תשלום: Ragil = עסקה רגילה
      }
    }
  },
  mounted() {
    // הוספת מאזין להודעות מהאייפרם
    window.addEventListener('message', this.handlePostMessage);
  },
  methods: {
    startDonation() {
      this.showIframe = true;
      
      // נחכה לטעינת האייפרם
      setTimeout(() => {
        this.iframeLoaded = true;
        
        // נמתין לטעינת האייפרם לפני שנשלח את הנתונים
        setTimeout(() => {
          this.postDataToIframe();
        }, 1000);
      }, 1000);
    },
    
    postDataToIframe() {
      if (!this.$refs.nedarimIframe) return;
      
      const iframeWindow = this.$refs.nedarimIframe.contentWindow;
      
      // הכנת הנתונים לשליחה לאייפרם
      const donation = {
        Mosad: this.nedarimConfiguration.Mosad,
        ApiValid: this.nedarimConfiguration.ApiValid,
        Zeout: '',                                    // מספר תעודת זהות
        FirstName: this.donationData.firstName,
        LastName: this.donationData.lastName,
        Street: this.donationData.street || '',
        City: this.donationData.city || '',
        Phone: this.donationData.phone,
        Mail: this.donationData.email || '',
        PaymentType: this.nedarimConfiguration.PaymentType,
        Amount: this.donationData.amount.toString(),
        Tashlumim: this.donationData.payments,
        Currency: this.nedarimConfiguration.Currency,
        Groupe: 'קמחא דפסחא',                         // קטגוריה
        Comment: this.donationData.dedication || '',
        Param1: '',                                   // טקסט חופשי
        Param2: '',                                   // טקסט חופשי
        CallBack: window.location.origin + '/api/donation-callback',  // כתובת לקבלת עדכון לשרת
        CallBackMailError: ''                         // מייל לשליחת התראות שגיאה
      };
      
      // שליחת הנתונים לאייפרם באמצעות PostNedarim
      iframeWindow.postMessage(JSON.stringify({
        action: 'PostNedarim',
        params: donation
      }), 'https://www.matara.pro');
    },
    
    handlePostMessage(event) {
      // וידוא שההודעה מגיעה מהדומיין של נדרים פלוס
      if (event.origin !== 'https://www.matara.pro') return;
      
      try {
        const data = JSON.parse(event.data);
        
        // התאמת גובה האייפרם
        if (data.action === 'height') {
          this.iframeHeight = data.height;
        }
        
        // קבלת תשובה מהאייפרם לאחר סיום העסקה
        if (data.action === 'TransactionResponse') {
          this.handleTransactionResponse(data.Response);
        }
      } catch (error) {
        console.error('שגיאה בעיבוד הודעה מהאייפרם:', error);
      }
    },
    
    handleTransactionResponse(response) {
      console.log('תשובה מהאייפרם:', response);
      
      // בדיקת סטטוס העסקה
      if (response.Status === 'True') {
        // עסקה הצליחה
        this.$router.push({
          path: '/donation-success',
          query: {
            transactionId: response.TransactionId,
            amount: this.donationData.amount
          }
        });
      } else {
        // עסקה נכשלה
        alert('התשלום נכשל: ' + response.ErrorMessage);
        this.showIframe = false;
      }
    }
  },
  beforeUnmount() {
    // הסרת המאזין כשהקומפוננטה מתפרקת
    window.removeEventListener('message', this.handlePostMessage);
  }
}
</script>

<style scoped>
.iframe-container {
  width: 100%;
  min-height: 400px;
  position: relative;
}

/* אנימציות */
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
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
  animation: pulse 1s infinite;
  box-shadow: 0 20px 25px -5px rgba(79, 70, 229, 0.3), 0 10px 10px -5px rgba(79, 70, 229, 0.2);
}

.btn-primary::after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: linear-gradient(to bottom, rgba(255,255,255,0.2), rgba(255,255,255,0));
  opacity: 0;
  transition: opacity 0.3s ease;
}

.btn-primary:hover::after {
  opacity: 1;
}

input:focus, select:focus, textarea:focus {
  animation: pulse 1.5s;
}

.text-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.card {
  background-color: white;
  padding: 2rem;
  border-radius: 0.75rem;
  transition: all 0.3s ease;
}

/* אפקט טוען כשלוחצים על כפתור שליחה */
@keyframes loading {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-button::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 20px;
  height: 20px;
  margin-top: -10px;
  margin-left: -10px;
  border-radius: 50%;
  border: 2px solid #ffffff;
  border-top-color: transparent;
  animation: loading 0.8s linear infinite;
}
</style> 