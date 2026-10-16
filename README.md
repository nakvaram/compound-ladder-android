# سود مرکب — اپلیکیشن اندرویدی

اپلیکیشن اندرویدی ماشین‌حساب «سود مرکب» که به‌صورت WebView **کاملاً آفلاین** کار می‌کند؛ یعنی خودِ ماشین‌حساب داخل اپ قرار دارد و هیچ نیازی به اینترنت نیست.

فایل APK این برنامه به‌صورت **خودکار توسط GitHub Actions** ساخته و در بخش Releases منتشر می‌شود.

## دانلود APK (بدون نیاز به Android Studio)

1. وارد صفحه [Releases](https://github.com/nakvaram/compound-ladder-android/releases/latest) شوید.
2. فایل `CompoundLadder-debug.apk` را از بخش Assets دانلود کنید.
3. روی گوشی، فایل را باز کنید. اگر پیام «نصب از منابع ناشناس» دیدید، آن را فعال کنید:
   **Settings → Install unknown apps → Allow from this source**
4. نصب تمام است — اپ «سود مرکب» با آیکون اختصاصی در فهرست برنامه‌ها ظاهر می‌شود.

- حداقل نسخه پشتیبانی‌شده: **Android 7.0 (API 24)**
- نسخه هدف: **Android 14 (API 34)**
- APK حالت debug برای استفاده شخصی و تست کاملاً مناسب است.

## امکانات اپ

- ماشین‌حساب کامل سود مرکب: پیش‌بینی سود + هدف معکوس، با جدول پلکانی ۱۲ ردیفه
- سه تم رنگی: تیره، روشن و سایبر
- اعداد فارسی و رابط کاربری راست‌به‌چپ
- دکمه‌های گام با نگه‌داشتن (تکرار خودکار) و لرزش (haptic)
- کاملاً آفلاین — بدون هیچ دسترسی اینترنتی

## بیلد خودکار (CI/CD)

هر بار که تغییری روی شاخه `main` پوش شود، GitHub Actions به‌صورت خودکار:

1. پروژه را با `./gradlew assembleDebug` بیلد می‌کند
2. فایل `CompoundLadder-debug.apk` را در Release نسخه `v1.0` به‌روزرسانی می‌کند

پس برای گرفتن نسخه جدید کافی است تغییرات را روی `main` پوش کنید و چند دقیقه بعد APK جدید را از همان صفحه Releases دانلود کنید.

## بیلد دستی از سورس

- **با Android Studio:** پوشه پروژه را Open کنید، پس از پایان Gradle Sync از منوی
  **Build → Build Bundle(s) / APK(s) → Build APK(s)** بگیرید. خروجی در
  `app/build/outputs/apk/debug/app-debug.apk` ساخته می‌شود.
- **با خط فرمان:**

  ```bash
  ./gradlew assembleDebug
  # خروجی: app/build/outputs/apk/debug/app-debug.apk
  ```

پیش‌نیازها: JDK 17 (بار اول، اینترنت برای دانلود Gradle و وابستگی‌ها لازم است).

## تغییر نام اپ

فایل `app/src/main/res/values/strings.xml` را ویرایش کنید و دوباره بیلد بگیرید:

```xml
<string name="app_name">نام دلخواه شما</string>
```

## ساختار پروژه

```
compound-ladder-android/
├── settings.gradle / build.gradle     ← تنظیمات Gradle (AGP 8.5.2 / Kotlin 1.9.24)
├── gradlew                            ← Gradle Wrapper نسخه 8.7
├── .github/workflows/android.yml      ← بیلد و انتشار خودکار APK
└── app/src/main/
    ├── AndroidManifest.xml            ← مانیفست
    ├── assets/index.html              ← خودِ ماشین‌حساب (کاملاً آفلاین)
    ├── java/com/compoundladder/app/MainActivity.kt
    └── res/                           ← آیکون‌ها، نام اپ، تم و رنگ‌ها
```

## لایسنس

MIT
