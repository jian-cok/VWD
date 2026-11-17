# Video to Dex Wallpaper (v2, Kotlin + Gradle)

Modul LSPosed untuk memutar video sebagai wallpaper desktop Samsung DeX. Ditulis ulang dari proyek smali v1.

## Cara build

**Paling mudah (tanpa PC): GitHub Actions**
1. Buat repo GitHub baru, unggah seluruh isi folder ini.
2. Buka tab *Actions* → *Build APK* → tunggu selesai → unduh artifact `VideoToDexWallpaper-apk`.

**Android Studio / PC:** buka folder ini, lalu `./gradlew :app:assembleRelease`
(butuh JDK 17 dan Android SDK 35). APK ada di `app/build/outputs/apk/release/`.

APK rilis ditandatangani dengan kunci *debug* agar langsung bisa dipasang. Untuk distribusi, ganti `signingConfig` di `app/build.gradle.kts`.

## Memasang
1. Uninstall v1 dulu (tanda tangan berbeda). Package tetap `zatool.videodex`.
2. Pasang APK, buka LSPosed → Modul → aktifkan, centang scope **Samsung DeX Launcher**.
3. Buka aplikasi → *Tambah video* → *Mulai ulang DeX Launcher*.

## Struktur
- `app/.../MainActivity.kt` — UI (pustaka video, pemutaran, alat).
- `app/.../provider/PrefProvider.kt` — jembatan ke DeX Launcher; hanya melayani aplikasi ini dan DeX Launcher; video disajikan lewat file descriptor read-only.
- `app/.../hook/` — hook LSPosed yang berjalan di proses DeX Launcher.
- `app/.../data/` — pengaturan dan pustaka video.
- `xposed-stub/` — stub API Xposed untuk compile saja (tidak masuk APK).
