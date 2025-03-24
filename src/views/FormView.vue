<template>
  <div class="min-h-screen py-12 bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom">
      <div class="text-center mb-8 bg-white p-8 rounded-2xl shadow-lg max-w-4xl mx-auto">
        <h1 class="text-4xl font-bold text-primary-700 mb-6 text-shadow">טופס מכירת חמץ</h1>
        <p class="text-lg text-gray-600 mb-6">מלאו את הטופס הבא לביצוע מכירת חמץ כהלכה</p>
        
        <!-- כפתורי שיתוף -->
        <!-- <div class="py-4">
          <ShareButtons 
            title="שתפו עם חברים ומשפחה" 
            text="טופס מכירת חמץ און-ליין - כולל עיון פרשטוש"
          />
        </div> -->
      </div>
      
      <div class="max-w-2xl mx-auto">
        <form @submit.prevent="handleSubmit" class="space-y-6">
          <!-- פרטים אישיים -->
          <div class="card rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
            <h2 class="text-2xl font-bold text-primary-800 mb-4">פרטים אישיים</h2>
            <div class="space-y-4">
              <div>
                <label class="form-label">שם פרטי <span class="text-red-500">*</span></label>
                <input type="text" v-model="formData.firstName" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400" required>
              </div>
              <div>
                <label class="form-label">שם משפחה <span class="text-red-500">*</span></label>
                <input type="text" v-model="formData.lastName" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400" required>
              </div>
              <div>
                <label class="form-label">טלפון</label>
                <input type="tel" v-model="formData.phone" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
              </div>
              <div>
                <label class="form-label">סוג מקום המכירה</label>
                <select v-model="formData.locationType" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
                  <option value="">נא בחרו</option>
                  <option value="home">בית</option>
                  <option value="store">חנות</option>
                  <option value="factory">מפעל</option>
                  <option value="other">אחר</option>
                </select>
              </div>
            </div>
          </div>
          
          <!-- כתובת -->
          <div class="card rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
            <h2 class="text-2xl font-bold text-primary-800 mb-4">כתובת</h2>
            <div class="space-y-4">
              <div>
                <label class="form-label">עיר מגורים <span class="text-red-500">*</span></label>
                <input type="text" v-model="formData.city" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400" required>
              </div>
              <div>
                <label class="form-label">רחוב <span class="text-red-500">*</span></label>
                <input type="text" v-model="formData.street" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400" required>
              </div>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div>
                  <label class="form-label">מספר בית <span class="text-red-500">*</span></label>
                  <input type="number" v-model="formData.houseNumber" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
                </div>
                <div>
                  <label class="form-label">כניסה</label>
                  <input type="text" v-model="formData.entrance" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
                </div>
                <div>
                  <label class="form-label">קומה</label>
                  <input type="text" v-model="formData.floor" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
                </div>
              </div>
              <div>
                <label class="form-label">מספר דירה</label>
                <input type="number" v-model="formData.apartmentNumber" class="form-input transition-all duration-300 focus:ring-2 focus:ring-primary-400">
              </div>
            </div>
          </div>
          
          <!-- פרטי החמץ -->
          <div class="card rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
            <h2 class="text-2xl font-bold text-primary-800 mb-4">מיקום החמץ</h2>
            <div class="space-y-4">
              <div>
                <label class="form-label">פירוט המקומות בהם נמצא החמץ <span class="text-red-500">*</span></label>
                <p class="text-sm text-gray-600 mb-2">
                  בשדה זה כתבו את המקומות בהם נמצא החמץ למכירה, לדוגמא "ארונות מטבח עליונים", "מחסן", "ארון שירות" וכדו'. אם המקומות מסומנים ניתן לכתוב "במקומות המסומנים"
                </p>
                <textarea v-model="formData.hametzLocations" class="form-input h-32 transition-all duration-300 focus:ring-2 focus:ring-primary-400" required></textarea>
              </div>
            </div>
          </div>
          
          <!-- אישורים -->
          <div class="card rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
            <h2 class="text-2xl font-bold text-primary-800 mb-4">אישור מינוי שליחות</h2>
            <div class="space-y-4">
              <div class="bg-primary-50 border-r-4 border-primary-500 p-4 rounded-lg">
                <p class="text-gray-700 leading-relaxed">
                  אני הח"מ נותן כוח ורשות להרב יוסף שמעון פרטוש שליט"א ועושה אותו שליח ומורשה במקומי לעשות מכירת חמץ לכל מיני חמץ ותערובות חמץ שלי ביום יד' ניסן תשפ"ה. ניתן לראות את נוסח השליחות המלא בהמשך הטופס
                </p>
              </div>
              <div class="flex items-start bg-gray-50 p-3 rounded-lg border border-gray-200">
                <input type="checkbox" v-model="formData.confirmations.rabbi" class="mt-1 h-5 w-5 text-primary-600 transition duration-150 ease-in-out" required>
                <label class="mr-2 text-gray-700 font-medium">
                  אני מאשר את מינוי השליחות <span class="text-red-500">*</span>
                </label>
              </div>
            </div>
          </div>
          
          <!-- הודעת שגיאה -->
          <div v-if="error" class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded-lg shadow" role="alert">
            <div class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-red-500 ml-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
              <div>
                <strong class="font-bold">שגיאה!</strong>
                <span class="block sm:inline"> {{ error }}</span>
              </div>
            </div>
          </div>

          <!-- הודעת הצלחה -->
          <div v-if="success" class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded-lg shadow" role="alert">
            <div class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-green-500 ml-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
              </svg>
              <div>
                <strong class="font-bold">הצלחה!</strong>
                <span class="block sm:inline"> {{ success }}</span>
              </div>
            </div>
          </div>

          <div class="text-center py-4">
            <button type="submit" class="btn-primary text-xl py-3 px-8 transform hover:scale-105 transition-transform duration-300" :disabled="isSubmitting" :class="{'opacity-70 cursor-not-allowed': isSubmitting}">
              <span v-if="isSubmitting" class="loading-spinner inline-block ml-2"></span>
              {{ isSubmitting ? 'שולח...' : 'שליחת הטופס' }}
            </button>
            <div class="mt-4">
              <router-link to="/" class="text-primary-600 hover:text-primary-700 font-medium">
                חזרה לדף הבית
              </router-link>
            </div>
          </div>
          
          <!-- תרומה לקמחא דפסחא -->
          <div class="text-center bg-white p-6 rounded-2xl shadow-lg mt-8">
            <h3 class="text-2xl font-bold text-primary-700 mb-4">מעוניינים לתרום לקמחא דפסחא?</h3>
            <p class="text-lg text-gray-600 mb-6">
              כולל שערי ניסים מחלק מאות סלי מזון לקראת חג הפסח, באו ליטול חלק!
            </p>
            <router-link to="/kimcha" class="text-xl py-3 px-8 inline-block transform hover:scale-105 transition-transform duration-300 rounded-lg font-bold text-white shadow-lg bg-gradient-to-r from-green-600 to-green-700 hover:from-green-700 hover:to-green-800 border border-green-600">
              לתרומה לקמחא דפסחא
            </router-link>
            
            <!-- כפתורי שיתוף בתחתית העמוד -->
            <div class="mt-8">
              <ShareButtons 
                title="שתפו עם חברים ומשפחה" 
                text="מכירת חמץ און-ליין וקמחא דפסחא - כולל שערי ניסים"
                size="medium"
              />
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import LogoHeader from '../components/LogoHeader.vue'
import ShareButtons from '../components/ShareButtons.vue'

export default {
  name: 'FormView',
  components: {
    LogoHeader,
    ShareButtons
  },
  data() {
    return {
      formData: {
        firstName: '',
        lastName: '',
        phone: '',
        locationType: 'home',
        city: '',
        street: '',
        houseNumber: '',
        entrance: '',
        floor: '',
        apartmentNumber: '',
        hametzLocations: '',
        confirmations: {
          rabbi: false
        }
      },
      isSubmitting: false,
      error: null,
      success: null,
      // החלף את ה-URL הזה עם ה-URL של ה-Web App שלך מ-Google Apps Script
      GOOGLE_SCRIPT_URL: 'https://script.google.com/macros/s/AKfycbxlbeRrsbFPoCzE4dFyBMnOL9UeMVXZljoLelNrIt82qRS0EJDF5h0m6XChBoAKAXzC/exec'
    }
  },
  methods: {
    async handleSubmit() {
      this.error = null;
      this.success = null;
      this.isSubmitting = true;

      try {
        const formData = new URLSearchParams();
        formData.append('data', JSON.stringify(this.formData));

        const response = await fetch(this.GOOGLE_SCRIPT_URL, {
          method: 'POST',
          mode: 'no-cors',
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded',
          },
          body: formData.toString()
        });

        this.success = 'הטופס נשלח בהצלחה!';
        this.resetForm();
        
        // ניווט לדף הצלחה
        setTimeout(() => {
          this.$router.push('/success');
        }, 2000);

      } catch (error) {
        console.error('Error:', error);
        this.error = 'אירעה שגיאה בשליחת הטופס. אנא נסו שוב מאוחר יותר.';
      } finally {
        this.isSubmitting = false;
      }
    },

    resetForm() {
      this.formData = {
        firstName: '',
        lastName: '',
        phone: '',
        locationType: '',
        city: '',
        street: '',
        houseNumber: '',
        entrance: '',
        floor: '',
        apartmentNumber: '',
        hametzLocations: '',
        confirmations: {
          rabbi: false
        }
      };
    }
  }
}
</script>

<style scoped>
.card {
  background-color: white;
  padding: 2rem;
  border-radius: 0.75rem;
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

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-spinner {
  width: 18px;
  height: 18px;
  border: 3px solid #ffffff;
  border-radius: 50%;
  border-top-color: transparent;
  animation: spin 0.8s linear infinite;
}
</style> 