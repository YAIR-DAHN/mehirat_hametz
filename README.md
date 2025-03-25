# 🌟 מכירת חמץ ותרומות קמחא דפסחא אונליין

<div dir="rtl" align="center">
  <h3>פלטפורמה מקוונת למכירת חמץ ותרומות קמחא דפסחא - כולל שערי ניסים</h3>
  <p>
    <a href="https://mehirat-hametz.vercel.app" target="_blank">צפייה באתר</a> • 
    <a href="#תכונות">תכונות</a> • 
    <a href="#טכנולוגיות">טכנולוגיות</a> • 
    <a href="#איך-להתחיל">איך להתחיל</a>
  </p>
</div>

---

## 📝 תיאור

פלטפורמה מקוונת המאפשרת למשתמשים למלא טופס מכירת חמץ ולתרום לקמחא דפסחא לקראת חג הפסח. האתר נבנה עבור כולל שערי ניסים בנשיאות הרב יוסף שמעון פרטוש שליט"א, ומציע ממשק משתמש ידידותי ונגיש לביצוע מצוות מכירת חמץ ותרומות קמחא דפסחא באופן מקוון.

## ✨ תכונות

- **טופס מכירת חמץ** - מילוי טופס אונליין למכירת חמץ, כולל פרטים אישיים, כתובת ופרטי החמץ
- **תרומה לקמחא דפסחא** - מערכת תרומות מאובטחת עם אפשרויות לתרומה חד פעמית או הוראת קבע
- **עיצוב רספונסיבי** - תמיכה מלאה בכל סוגי המכשירים (נייד, טאבלט, מחשב)
- **שיתוף חברתי** - אפשרות לשיתוף בוואטסאפ, פייסבוק, אימייל והעתקת קישור
- **ממשק RTL מלא** - תמיכה מלאה בעברית וכיוון טקסט מימין לשמאל
- **מאובטח** - עיבוד תשלומים מאובטח באמצעות ממשק נדרים פלוס

## 🛠️ טכנולוגיות

<div dir="ltr">

- **Frontend:**
  - Vue.js 3 (Composition API)
  - Vite
  - TailwindCSS
  - Vue Router

- **Deployment:**
  - Vercel

- **Integrations:**
  - Nedarim Plus API (מערכת תשלומים)
  - WhatsApp/Facebook Web Share APIs

</div>

## 🚀 איך להתחיל

### התקנה

```bash
# שיבוט המאגר
git clone https://github.com/YAIR-DAHN/mehirat_hametz.git
cd mehirat_hametz

# התקנת תלויות
npm install

# הפעלת שרת פיתוח
npm run dev
```

### פריסה לשרת

האתר מוגדר לעבודה עם Vercel. כל העלאה לענף הראשי תגרום לפריסה אוטומטית.

```bash
# בנייה לייצור
npm run build
```

## 🌐 ניתוב עמודים

- **`/`** - דף הבית עם מידע על מכירת חמץ וקישורים מהירים
- **`/form`** - טופס מכירת חמץ
- **`/kimcha`** - דף תרומה לקמחא דפסחא
- **`/success`** - דף אישור השלמת מכירת חמץ
- **`/donation-success`** - דף אישור השלמת תרומה

## 🔧 תצורה ייחודית ל-Vercel

הפרויקט כולל קובץ `vercel.json` המגדיר כללי הפניה (rewrites) לתמיכה בניתוב צד-לקוח. זה מאפשר גישה ישירה ל-URL מסוימים (לדוגמא: `/kimcha`) ללא שגיאות 404:

```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

## 📄 רישיון

כל הזכויות שמורות © 2025 ל Y.D. Systems 
