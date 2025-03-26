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
          <!-- <div class="py-4">
            <ShareButtons 
              title="עזרו לנו להפיץ את המצווה" 
              text="סייעו למשפחות נזקקות בחג הפסח - קמחא דפסחא של כולל שערי ניסים"
              size="large"
            />
          </div> -->
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
          <p class="text-gray-600 mb-6 text-center">התרומות מוכרות לצורכי מס לפי סעיף 46</p>
          
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
                <input 
                  type="tel" 
                  v-model="donationData.phone" 
                  class="form-input" 
                  required
                  pattern="^0[0-9]{8,9}$"
                  @input="validatePhone"
                  :class="{'border-red-500': phoneError}"
                >
                <span v-if="phoneError" class="text-red-500 text-sm">מספר טלפון לא תקין</span>
              </div>
              <div>
                <label class="form-label">דוא"ל</label>
                <input 
                  type="email" 
                  v-model="donationData.email" 
                  class="form-input"
                  @input="validateEmail"
                  :class="{'border-red-500': emailError}"
                >
                <div class="text-sm text-gray-500 mt-1 mr-2">
                  <span>קבלה תישלח לדואר האלקטרוני</span>
                  <span v-if="emailError" class="text-red-500 block">* כתובת מייל לא תקינה</span>
                </div>
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

                <div class="grid grid-cols-1 md:grid-cols-2 gap-3 mb-3">
                  <button 
                    type="button"
                    class="py-3 px-4 border rounded-lg text-lg transition-all duration-300 transform hover:scale-105" 
                    :class="donationData.amount === 600 ? 'bg-primary-100 border-primary-500 font-bold shadow-lg scale-105' : 'border-gray-300 hover:border-primary-400'"
                    @click="setAmount(600)"
                  >
                    סל מלא - ₪600
                  </button>
                  <button 
                    type="button"
                    class="py-3 px-4 border rounded-lg text-lg transition-all duration-300 transform hover:scale-105" 
                    :class="donationData.amount === 300 ? 'bg-primary-100 border-primary-500 font-bold shadow-lg scale-105' : 'border-gray-300 hover:border-primary-400'"
                    @click="setAmount(300)"
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
                    :class="donationData.amount === amount ? 'bg-primary-100 border-primary-500 shadow-lg scale-105' : 'border-gray-300 hover:border-primary-400'"
                    @click="setAmount(amount)"
                  >
                    ₪{{ amount }}
                  </button>
                </div>
                  <label class="form-label">סכום תרומה <span class="text-red-500">*</span></label>
                <!-- תצוגת הסכום הנבחר -->
                <div class="text-center mb-6 overflow-hidden">
                  <div class="text-5xl font-bold text-primary-700 mb-2">
                    ₪{{ formattedAmount }}
                  </div>
                  <div class="text-gray-500" v-if="donationData.payments > 1 && donationData.paymentType === 'Ragil'">
                    {{ donationData.payments }} תשלומים של ₪{{ (donationData.amount / donationData.payments).toFixed(0) }}
                  </div>
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

              <!-- סוג תשלום -->
              <div class="mb-6">
                <label class="form-label">סוג תשלום</label>
                <div class="grid grid-cols-2 gap-3">
                  <button 
                    type="button"
                    class="w-full py-3 px-4 border rounded-lg text-lg transition-all duration-300" 
                    :class="donationData.paymentType === 'Ragil' ? 'bg-primary-100 border-primary-500 font-bold shadow-lg' : 'border-gray-300 hover:border-primary-400'"
                    @click="setPaymentType('Ragil')"
                  >
                    תרומה חד פעמית
                  </button>
                  <div>
                    <button 
                      type="button"
                      class="w-full py-3 px-4 border rounded-lg text-lg transition-all duration-300" 
                      :class="donationData.paymentType === 'HK' ? 'bg-primary-100 border-primary-500 font-bold shadow-lg' : 'border-gray-300 hover:border-primary-400'"
                      @click="setPaymentType('HK')"
                    >
                      הוראת קבע חודשית
                    </button>
                    <div v-if="donationData.paymentType === 'HK'" class="text-sm text-gray-500 mt-1 mr-2">
                      חיוב חודשי קבוע בכרטיס האשראי
                    </div>
                  </div>
                </div>
              </div>

              <div>
                <label class="form-label">{{ donationData.paymentType === 'Ragil' ? 'מספר תשלומים' : 'משך הוראת הקבע' }}</label>
                <select 
                  v-if="donationData.paymentType === 'Ragil'"
                  v-model="donationData.payments" 
                  class="form-input"
                >
                  <option value="1">תשלום אחד</option>
                  <option value="2">2 תשלומים</option>
                  <option value="3">3 תשלומים</option>
                  <option value="6">6 תשלומים</option>
                  <option value="12">12 תשלומים</option>
                </select>
                <select 
                  v-else
                  v-model="donationData.hkPeriod" 
                  class="form-input"
                >
                  <option :value="0">ללא הגבלה</option>
                  <option :value="3">3 חודשים</option>
                  <option :value="6">6 חודשים</option>
                  <option :value="12">שנה</option>
                  <option :value="24">שנתיים</option>
                  <option :value="36">3 שנים</option>
                  <option :value="60">5 שנים</option>
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
            <!-- תצוגת סיכום לפני התשלום -->
            <div class="bg-primary-50 p-6 rounded-lg mb-6">
              <h3 class="text-2xl font-bold text-primary-800 mb-4 text-center">סיכום התרומה</h3>
              <div class="space-y-3 text-lg">
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">סכום התרומה:</span>
                  <span class="font-bold text-primary-700">₪{{ formattedAmount }}</span>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-gray-600">סוג תשלום:</span>
                  <span class="font-bold text-primary-700">{{ donationData.paymentType === 'Ragil' ? 'תשלום חד פעמי' : 'הוראת קבע חודשית' }}</span>
                </div>
                <div class="flex justify-between items-center" v-if="donationData.paymentType === 'Ragil' && donationData.payments > 1">
                  <span class="text-gray-600">מספר תשלומים:</span>
                  <span class="font-bold text-primary-700">{{ donationData.payments }}</span>
                </div>
                <div class="flex justify-between items-center" v-if="donationData.paymentType === 'Ragil' && donationData.payments > 1">
                  <span class="text-gray-600">סכום לתשלום:</span>
                  <span class="font-bold text-primary-700">₪{{ (donationData.amount / donationData.payments).toFixed(0) }} × {{ donationData.payments }}</span>
                </div>
                <div class="flex justify-between items-center" v-if="donationData.paymentType === 'HK'">
                  <span class="text-gray-600">משך הוראת הקבע:</span>
                  <span class="font-bold text-primary-700">{{ donationData.hkPeriod === 0 ? 'ללא הגבלה' : formatHkPeriod(donationData.hkPeriod) }}</span>
                </div>
                <div class="flex justify-between items-center" v-if="donationData.dedication">
                  <span class="text-gray-600">הקדשה:</span>
                  <span class="font-bold text-primary-700">{{ donationData.dedication }}</span>
                </div>
                <div class="border-t border-primary-200 mt-4 pt-4">
                  <div class="flex justify-between items-center text-xl">
                    <span class="font-bold text-primary-800">{{ donationData.paymentType === 'HK' ? 'סכום חודשי:' : 'סה"כ לתשלום:' }}</span>
                    <span class="font-bold text-primary-800">₪{{ formattedAmount }}</span>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- האייפריים להכנסת פרטי אשראי -->
            <iframe 
              v-if="iframeLoaded" 
              ref="nedarimIframe" 
              id="nedarimIframe"
              src="https://www.matara.pro/nedarimplus/iframe/"
              width="100%" 
              style="height: 350px;"
              frameborder="0"
              allow="payment"
            ></iframe>
            
            <!-- כפתור התשלום -->
            <div v-if="iframeLoaded && !isProcessingPayment" class="text-center mt-2 mb-8">
              <button 
                type="button" 
                @click="executePayment"
                class="bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-12 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg text-xl"
                :disabled="isProcessingPayment"
              >
                ביצוע תשלום
              </button>
            </div>
            
            <!-- טוען או שגיאות -->
            <div v-if="!iframeLoaded" class="text-center py-8">
              <div class="inline-block animate-spin rounded-full h-8 w-8 border-b-2 border-primary-600"></div>
              <p class="mt-4 text-gray-600">טוען את עמוד התשלום...</p>
            </div>
            
            <!-- אנימציית המתנה בזמן סליקה -->
            <div v-if="isProcessingPayment" class="text-center py-4">
              <div class="inline-block animate-spin rounded-full h-10 w-10 border-b-2 border-primary-600"></div>
              <p class="mt-2 text-gray-600 text-lg">מבצע חיוב, נא להמתין...</p>
            </div>
            
            <!-- הודעת שגיאה מהעסקה -->
            <div v-if="paymentError" class="bg-red-50 p-4 rounded-lg mt-4 text-red-700">
              <div class="font-bold mb-2 text-center">{{ paymentError }}</div>
              
              <div class="text-sm mt-4">
                <div class="font-semibold mb-1">פרטי תרומה:</div>
                <pre class="bg-gray-100 p-2 rounded overflow-auto text-xs">{{ JSON.stringify(donationData, null, 2) }}</pre>
              </div>
            </div>
            
            <!-- הודעת הצלחה -->
            <div v-if="paymentSuccess" class="bg-green-50 p-6 rounded-lg mt-6 text-center">
              <div class="text-5xl mb-4 text-green-500">✅</div>
              <h3 class="text-2xl font-bold text-green-700 mb-2">התשלום התקבל בהצלחה!</h3>
              <p class="text-gray-600 mb-4">תודה על תרומתך לקמחא דפסחא, קבלה נשלחה לדואר האלקטרוני.</p>
              
              <!-- כפתורי שיתוף -->
              <div class="py-4">
                <ShareButtons 
                  title="תרמתי כעת לקמחא דפסחא" 
                  text="הצטרפו אלי לתרומה לקמחא דפסחא לפסח - כולל שערי ניסים"
                />
              </div>
              
              <div class="mt-4">
                <router-link to="/" class="text-primary-600 hover:text-primary-700 font-bold">
                  חזרה לדף הבית
                </router-link>
              </div>
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
        amount: 600,
        payments: '1',
        dedication: '',
        paymentType: 'Ragil', // Ragil = חד פעמי, HK = הוראת קבע
        hkPeriod: 0 // 0 = ללא הגבלה, אחרת מספר חודשים
      },
      showIframe: false,
      iframeLoaded: false,
      nedarimConfiguration: {
        Mosad: '7001292',         // מזהה מוסד בנדרים פלוס
        ApiValid: 'LgbGNqwumA',   // מפתח אימות
        Currency: '1',            // 1 = שקל, 2 = דולר
        PaymentType: 'Ragil',     // סוג תשלום: Ragil = עסקה רגילה
      },
      animatingAmount: false,
      phoneError: false,
      targetAmount: 0,
      currentDisplayAmount: 0,
      paymentError: null,
      isProcessingPayment: false,
      paymentSuccess: false,
      paymentTimeout: null,
      emailError: false
    }
  },
  computed: {
    formattedAmount() {
      const amount = this.animatingAmount ? Math.floor(this.currentDisplayAmount) : this.donationData.amount;
      return amount.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
    }
  },
  mounted() {
    // הוספת מאזין להודעות מהאייפרם
    window.addEventListener('message', this.handlePostMessage);
    
    // הגדרת URL של צד שלישי לתשלום כשיש צורך להפנות למסך תשלום חיצוני
    window.redirectToPayment = (url) => {
      console.log('מפנה לדף תשלום חיצוני:', url);
      window.open(url, '_blank');
    };
  },
  methods: {
    validatePhone() {
      const phoneRegex = /^0[0-9]{8,9}$/
      this.phoneError = !phoneRegex.test(this.donationData.phone)
    },
    validateEmail() {
      if (!this.donationData.email) {
        this.emailError = false;
        return;
      }
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      this.emailError = !emailRegex.test(this.donationData.email)
    },
    setPaymentType(type) {
      this.donationData.paymentType = type
      this.nedarimConfiguration.PaymentType = type
      // אם זו הוראת קבע, נאפס את מספר התשלומים ל-1
      if (type === 'HK') {
        this.donationData.payments = '1'
        if (this.donationData.hkPeriod === undefined) {
          this.donationData.hkPeriod = 0 // ללא הגבלה
        }
      }
    },
    setHkPeriod(period) {
      this.donationData.hkPeriod = period
    },
    startDonation() {
      // בדיקת תקינות מספר טלפון ומייל לפני שליחה
      this.validatePhone();
      if (this.donationData.email) {
        this.validateEmail();
      }
      
      if (this.phoneError) {
        alert('אנא הזן מספר טלפון תקין');
        return;
      }
      
      if (this.emailError) {
        alert('אנא הזן כתובת מייל תקינה');
        return;
      }
      
      this.showIframe = true;
      this.paymentError = null;
      this.isProcessingPayment = false;
      this.paymentSuccess = false;
      
      // טעינת האייפריים
      setTimeout(() => {
        this.iframeLoaded = true;
      }, 1000);
    },
    executePayment() {
      // ביצוע התשלום כאשר לוחצים על כפתור התשלום
      this.paymentError = null
      this.isProcessingPayment = true
      
      // הגדרת טיימאאוט למקרה שלא מתקבלת תשובה מהאייפריים
      this.paymentTimeout = setTimeout(() => {
        if (this.isProcessingPayment) {
          this.isProcessingPayment = false;
          this.paymentError = 'לא התקבלה תשובה מהשרת. נסה שנית או פנה לתמיכה.';
          console.error('תם הזמן המוקצב לקבלת תשובה מהאייפריים');
        }
      }, 20000); // 20 שניות טיימאאוט
      
      // שליחת הנתונים לאייפריים
      this.postDataToIframe();
    },
    postDataToIframe() {
      if (!this.$refs.nedarimIframe) {
        console.error('האייפריים לא נמצא');
        this.isProcessingPayment = false;
        clearTimeout(this.paymentTimeout);
        this.paymentError = 'אירעה שגיאה בתהליך התשלום. נסה שנית.';
        return;
      }
      
      const iframeWindow = this.$refs.nedarimIframe.contentWindow;
      if (!iframeWindow) {
        console.error('לא ניתן לגשת לחלון האייפריים');
        this.isProcessingPayment = false;
        clearTimeout(this.paymentTimeout);
        this.paymentError = 'אירעה שגיאה בתהליך התשלום. נסה שנית.';
        return;
      }
      
      // הגדרת אובייקט התרומה
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
        PaymentType: this.donationData.paymentType,   // Ragil או HK
        Amount: this.donationData.amount.toString(),
        Tashlumim: this.donationData.paymentType === 'HK' && this.donationData.hkPeriod === 0 ? '' : this.donationData.payments,  // אם הוראת קבע ללא הגבלה, להשאיר ריק
        Currency: this.nedarimConfiguration.Currency, // 1 = שקל, 2 = דולר
        Groupe: 'קמחא דפסחא',                         // קטגוריה
        Comment: this.donationData.dedication || '',
        Param1: this.donationData.paymentType === 'HK' ? 
                (this.donationData.hkPeriod > 0 ? this.formatHkPeriod(this.donationData.hkPeriod) : 'ללא הגבלה') : '',
        Param2: '',                                   // טקסט חופשי
        CallBack: '',                                 // השארת שדה ריק - אין צורך בקאלבק 
        CallBackMailError: ''                         // מייל לשליחת התראות שגיאה
      };
      
      console.log('שולח נתונים לאייפרם:', donation);
      
      try {
        // שליחת הנתונים לאייפרם לפי דוגמת האתר - בדיוק כמו בדוגמא
        const message = {
          Name: 'FinishTransaction2',
          Value: donation
        };
        
        console.log('שולח הודעה לאייפריים:', message);
        
        // שליחה באופן ישיר, כמו בדוגמא, בלי JSON.stringify
        iframeWindow.postMessage(message, 'https://www.matara.pro');
      } catch (error) {
        console.error('שגיאה בשליחת נתונים לאייפריים:', error);
        this.isProcessingPayment = false;
        clearTimeout(this.paymentTimeout);
        this.paymentError = 'אירעה שגיאה בתהליך התשלום: ' + error.message;
      }
    },
    
    handlePostMessage(event) {
      // וידוא שההודעה מגיעה מהדומיין של נדרים פלוס
      if (event.origin !== 'https://www.matara.pro') {
        console.log('התקבלה הודעה מדומיין לא מורשה:', event.origin);
        return;
      }
      
      try {
        console.log('התקבלה הודעה מהאייפרם:', event.data);
        
        // אם זה אובייקט ישיר
        const data = event.data;
        
        console.log('נתוני הודעה מפורסרים:', data);
        
        // הפניה לדף תשלום חיצוני (למשל PayPal)
        if (data.Name === 'RedirectTo' || data.action === 'RedirectTo') {
          const url = data.Value || data.url;
          if (window.redirectToPayment && url) {
            console.log('מפנה לדף תשלום חיצוני:', url);
            window.redirectToPayment(url);
          }
        }
        
        // עדכון סטטוס תשלום
        if (data.Name === 'PaymentUpdate' || data.action === 'PaymentUpdate') {
          console.log('עדכון סטטוס תשלום:', data);
          // אפשר להוסיף כאן לוגיקה לעדכון ממשק המשתמש
        }
        
        // קבלת תשובה מהאייפרם לאחר סיום העסקה
        if (data.Name === 'TransactionResponse' || data.action === 'TransactionResponse') {
          const response = data.Value || data.Response;
          console.log('התקבלה תשובת עסקה:', response);
          
          // ביטול הטיימאאוט כי קיבלנו תשובה
          if (this.paymentTimeout) {
            clearTimeout(this.paymentTimeout);
          }
          
          this.handleTransactionResponse(response);
        }
        
        // הודעת שגיאה מהאייפרם
        if (data.Name === 'Error' || data.action === 'Error') {
          const errorMsg = data.Value || data.ErrorMessage;
          console.error('שגיאה מנדרים פלוס:', errorMsg);
          
          // ביטול הטיימאאוט כי קיבלנו תשובה
          if (this.paymentTimeout) {
            clearTimeout(this.paymentTimeout);
          }
          
          this.isProcessingPayment = false;
          this.paymentError = 'אירעה שגיאה: ' + errorMsg;
        }
        
        // הודעת שגיאה בוולידציה
        if (data.Name === 'ValidationError' || data.action === 'ValidationError') {
          const errors = data.Value || data.Errors;
          console.error('שגיאת וולידציה:', errors);
          
          // ביטול הטיימאאוט כי קיבלנו תשובה
          if (this.paymentTimeout) {
            clearTimeout(this.paymentTimeout);
          }
          
          this.isProcessingPayment = false;
          
          let errorMsg = 'נא לתקן את השגיאות הבאות:\n';
          
          if (Array.isArray(errors)) {
            errors.forEach(err => {
              errorMsg += `- ${err.FieldName}: ${err.ErrorMessage}\n`;
            });
          }
          
          this.paymentError = errorMsg;
          setTimeout(() => {
            this.showIframe = false; // חזרה לטופס
          }, 3000);
        }
      } catch (error) {
        console.error('שגיאה בעיבוד הודעה מהאייפרם:', error, event.data);
        this.isProcessingPayment = false;
        if (this.paymentTimeout) {
          clearTimeout(this.paymentTimeout);
        }
        this.paymentError = 'אירעה שגיאה בעיבוד התשובה מהשרת';
      }
    },
    
    handleTransactionResponse(response) {
      console.log('מעבד תשובה מהאייפרם:', response);
      this.isProcessingPayment = false;
      
      // בדיקת סטטוס העסקה - בתצוגת המשתמש, תמיד להציג הצלחה כשסטטוס הוא OK
      if (response && (response.Status === 'True' || response.Status === 'OK')) {
        // עסקה הצליחה
        this.paymentSuccess = true;
        
        // מעבר לדף אישור לאחר השהייה קצרה
        setTimeout(() => {
          this.$router.push({
            path: '/donation-success',
            query: {
              transactionId: response.TransactionId || response.Confirmation || 'unknown',
              amount: this.donationData.amount,
              type: this.donationData.paymentType,
              period: this.donationData.paymentType === 'HK' ? 
                      (this.donationData.hkPeriod === 0 ? 'ללא הגבלה' : this.formatHkPeriod(this.donationData.hkPeriod)) : '',
              payments: this.donationData.payments
            }
          });
        }, 2000);
      } else if (response && response.Status === 'Error') {
        // עסקה נכשלה עם שגיאה מוגדרת
        this.paymentError = 'התשלום נכשל: ' + (response.Message || response.ErrorMessage || 'אירעה שגיאה בתהליך התשלום');
      } else {
        // עסקה נכשלה ללא פרטים או שגיאה כללית
        const errorMsg = response ? 
                         (response.Message || response.ErrorMessage || 'אירעה שגיאה בתהליך התשלום') : 
                         'התשלום נכשל ללא פרטי שגיאה';
        this.paymentError = 'התשלום נכשל: ' + errorMsg;
      }
    },
    setAmount(amount) {
      if (this.animatingAmount) return;
      
      this.animatingAmount = true;
      this.targetAmount = amount;
      this.currentDisplayAmount = this.donationData.amount;
      
      // מספר הצעדים והמשך זמן
      const duration = 1000; // משך האנימציה במילישניות
      const fps = 60;
      const steps = duration / (1000 / fps);
      
      let step = 0;
      const startValue = this.donationData.amount;
      const changeInValue = this.targetAmount - startValue;
      
      const animateAmount = () => {
        step++;
        
        // נוסחת easeOutQuad לאנימציה חלקה
        const progress = 1 - Math.pow(1 - step / steps, 2);
        this.currentDisplayAmount = startValue + changeInValue * progress;
        
        if (step < steps) {
          requestAnimationFrame(animateAmount);
        } else {
          // סיום האנימציה
          this.donationData.amount = this.targetAmount;
          this.currentDisplayAmount = this.targetAmount;
          this.animatingAmount = false;
        }
      };
      
      requestAnimationFrame(animateAmount);
    },
    formatHkPeriod(months) {
      if (months === 12) return 'שנה';
      if (months === 24) return 'שנתיים';
      if (months === 36) return '3 שנים';
      if (months === 60) return '5 שנים';
      return months + ' חודשים';
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

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* הוספת אנימציות לכפתורים */
.btn-primary, button {
  transition: all 0.3s ease;
}

.btn-primary:hover, button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.btn-primary:active, button:active {
  transform: translateY(1px);
}

/* שיפור עיצוב הטופס */
.form-input:focus {
  transform: scale(1.02);
}

.iframe-container {
  transition: all 0.5s ease;
}

/* הסתרת אנימציית המספרים */
.text-5xl {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}
</style> 
