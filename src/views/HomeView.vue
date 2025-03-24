<template>
  <div class="min-h-screen bg-gradient-to-b from-gray-50 to-primary-50">
    <LogoHeader />

    <div class="container-custom py-8 md:py-12">
      <div class="max-w-4xl mx-auto">
        <!-- Hero Section -->
        <div class="text-center mb-12 bg-white p-8 rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <h1 class="text-4xl md:text-5xl font-bold text-primary-700 mb-6 text-shadow">
            מכירת חמץ<br>מקוונת
          </h1>
          <p class="text-xl md:text-2xl text-gray-600 mb-8">
            מכירת חמץ מקוונת, פשוטה ומהירה לפני חג הפסח. המתקיימת על ידי כולל שערי ניסים בנשיאות הרב יוסף שמעון פרטוש שליט"א
          </p>
          <div class="flex flex-col md:flex-row gap-4 justify-center items-center">
            <router-link to="/form" class="btn-primary text-xl py-3 px-8 w-full md:w-auto transform hover:scale-105 transition-transform duration-300">
              למילוי טופס המכירה
            </router-link>
            <router-link to="/kimcha" class="text-xl py-3 px-8 w-full md:w-auto transform hover:scale-105 transition-transform duration-300 rounded-lg font-bold text-white shadow-lg bg-gradient-to-r from-green-600 to-green-700 hover:from-green-700 hover:to-green-800 border border-green-600">
              תרומה לקמחא דפסחא
            </router-link>
            <button @click="showMoreInfo = true" class="btn-secondary text-xl py-3 px-8 w-full md:w-auto transform hover:scale-105 transition-transform duration-300">
              מידע נוסף
            </button>
          </div>
          
          <!-- כפתורי שיתוף -->
          <div class="mt-8">
            <ShareButtons 
              title="עזרו לנו להפיץ את המצווה" 
              text="מכירת חמץ מקוונת של כולל שערי ניסים - הזדרזו למלא את הטופס לפני פסח!"
              size="large"
            />
          </div>
        </div>

        <!-- תמונת חמץ -->
        <!-- <div class="card mb-8 overflow-hidden rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <img src="../assets/images/hametz.jpeg" alt="חמץ" class="w-full h-96 object-cover rounded-lg hover:scale-105 transition-transform duration-700">
        </div> -->

        <!-- איך זה עובד -->
        <div class="card mb-8 rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <h2 class="text-3xl font-bold text-primary-800 mb-6 text-center">איך זה עובד?</h2>
          <div class="grid md:grid-cols-3 gap-8">
            <div class="text-center transform hover:scale-105 transition-transform duration-300">
              <div class="bg-primary-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4 shadow-md">
                <span class="text-2xl font-bold text-primary-600">1</span>
              </div>
              <h3 class="text-xl font-bold text-gray-800 mb-2">מלאו את הטופס</h3>
              <p class="text-gray-600">מלאו את הפרטים הנדרשים בטופס המכירה</p>
            </div>
            <div class="text-center transform hover:scale-105 transition-transform duration-300">
              <div class="bg-primary-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4 shadow-md">
                <span class="text-2xl font-bold text-primary-600">2</span>
              </div>
              <h3 class="text-xl font-bold text-gray-800 mb-2">מינוי הרב</h3>
              <p class="text-gray-600">הרב יוסף שמעון פרטוש שליט"א ימונה כשליח למכירת החמץ</p>
            </div>
            <div class="text-center transform hover:scale-105 transition-transform duration-300">
              <div class="bg-primary-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4 shadow-md">
                <span class="text-2xl font-bold text-primary-600">3</span>
              </div>
              <h3 class="text-xl font-bold text-gray-800 mb-2">מכירת החמץ</h3>
              <p class="text-gray-600">הרב יבצע את מכירת החמץ לגוי בהתאם להלכה</p>
            </div>
          </div>
        </div>

        <!-- אזהרה -->
        <div class="bg-yellow-50 border-r-4 border-yellow-400 p-6 mb-8 rounded-lg shadow-md transform hover:shadow-lg transition-all duration-300">
          <p class="text-yellow-700 text-lg">
            <strong class="text-yellow-800">חשוב לדעת:</strong> יש למלא את הטופס לא יאוחר מיום י"ג בניסן תשפ"ה, לפני זמן איסור חמץ.
          </p>
        </div>

        <!-- Call to Action -->
        <div class="text-center p-8 bg-white rounded-2xl shadow-lg transform hover:shadow-xl transition-all duration-300">
          <h2 class="text-3xl font-bold text-primary-700 mb-4 text-shadow">
            אל תחכו לרגע האחרון
          </h2>
          <p class="text-xl text-gray-600 mb-6">
            מלאו את הטופס עכשיו והבטיחו את מכירת החמץ שלכם בהתאם להלכה
          </p>
          <div class="mb-6">
            <router-link to="/form" class="btn-primary text-xl py-3 px-8 inline-block transform hover:scale-105 transition-transform duration-300">
              למילוי טופס המכירה
            </router-link>
          </div>
          
          <!-- הוספת אפשרות שיתוף -->
          <div class="mt-4">
            <ShareButtons 
              title="שתפו עם חברים ומשפחה" 
              text="האם מילאתם כבר את טופס מכירת החמץ? לחצו כאן לטופס מכירת חמץ מקוון של כולל שערי ניסים"
            />
          </div>
        </div>

        <!-- מידע נוסף - מודל -->
        <div v-if="showMoreInfo" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4" @click="showMoreInfo = false">
          <div class="bg-white rounded-lg max-w-2xl w-full max-h-[90vh] overflow-y-auto" @click.stop>
            <div class="p-6">
              <div class="flex justify-between items-center mb-4">
                <h2 class="text-2xl font-bold text-primary-800">מידע על מכירת חמץ</h2>
                <button @click="showMoreInfo = false" class="text-gray-500 hover:text-gray-700 transform hover:rotate-90 transition-transform duration-300">
                  <span class="text-2xl">&times;</span>
                </button>
              </div>
              
              <div class="space-y-6">
                <div>
                  <h3 class="text-xl font-bold text-primary-700 mb-2">מהי מכירת חמץ?</h3>
                  <p class="text-gray-600 leading-relaxed">
                    מכירת חמץ היא פתרון הלכתי לבעיית החמץ בפסח. על פי ההלכה היהודית, אסור ליהודי להחזיק חמץ ברשותו במהלך חג הפסח. באמצעות מכירת החמץ לגוי, אנו מקיימים את המצווה ונמנעים מאיסור בל יראה ובל ימצא.
                  </p>
                </div>
                
                <div>
                  <h3 class="text-xl font-bold text-primary-700 mb-2">דוגמא לשטר הרשאה</h3>
                  <img src="../assets/images/tofes.png" alt="שטר הרשאה למכירת חמץ" class="w-full h-auto rounded-lg shadow-md">
                </div>

                <div>
                  <h3 class="text-xl font-bold text-primary-700 mb-2">מועד אחרון למכירה</h3>
                  <p class="text-gray-600 leading-relaxed">
                    יש למלא את הטופס לא יאוחר מיום י"ג בניסן תשפ"ה
                  </p>
                </div>

                <div class="text-center mt-8">
                  <router-link to="/form" class="btn-primary text-xl py-3 px-8 transform hover:scale-105 transition-transform duration-300">
                    למילוי טופס המכירה
                  </router-link>
                </div>
                
                <!-- הוספת אפשרות שיתוף -->
                <div class="mt-6">
                  <ShareButtons 
                    title="שתפו מידע זה" 
                    text="מידע חשוב על מכירת חמץ לפסח - כולל שערי ניסים"
                    size="small"
                  />
                </div>
              </div>
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
  name: 'HomeView',
  components: {
    LogoHeader,
    ShareButtons
  },
  data() {
    return {
      showMoreInfo: false
    }
  }
}
</script>

<style>
.btn-secondary {
  @apply bg-white text-primary-700 border-2 border-primary-700 rounded-lg hover:bg-primary-50 transition-all duration-300;
  box-shadow: 0 4px 6px -1px rgba(79, 70, 229, 0.1), 0 2px 4px -1px rgba(79, 70, 229, 0.06);
}

.btn-secondary:hover {
  box-shadow: 0 10px 15px -3px rgba(79, 70, 229, 0.2), 0 4px 6px -2px rgba(79, 70, 229, 0.1);
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
</style> 