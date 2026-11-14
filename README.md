# Smart CB Analyzer - Aplikasi Android

Aplikasi ini membuka website yang disajikan ESP32 (`http://192.168.4.1`) di dalam aplikasi,
sehingga tampilannya sama dengan versi web dan ikut berubah jika `web_ui.h` di firmware diperbarui.

Tambahan dibanding membuka lewat browser:
- Tombol **Sambungkan otomatis** ke WiFi `SmartCB-Analyzer` (Android 10+).
- Aplikasi dipaksa memakai WiFi alat walau Android menganggapnya "tanpa internet".
- Layar tetap menyala selama aplikasi dibuka (hitung mundur butuh koneksi aktif).
- Ikon aplikasi, layar sambung dengan animasi, dan **Unduh CSV** langsung ke folder Download.

## Cara paling mudah: dapat file APK tanpa install Android Studio (lewat GitHub)

1. Buat akun gratis di https://github.com lalu klik **New repository** (nama bebas, misal `smartcb-app`), pilih Public atau Private.
2. Ekstrak `SmartCBAnalyzerApp.zip`. Buka folder hasil ekstrak, lalu **seret semua isinya** (termasuk folder `.github`) ke halaman repository
   (**Add file > Upload files**), lalu klik **Commit changes**.
   - Jika folder `.github` tidak ikut terunggah: klik **Add file > Create new file**, ketik nama `.github/workflows/build-apk.yml`,
     tempel isi file `build-apk.yml.txt`, lalu Commit.
3. Buka tab **Actions**. Proses **Build APK** berjalan otomatis (sekitar 3-6 menit). Jika tidak jalan, pilih **Build APK > Run workflow**.
4. Setelah centang hijau, klik proses itu, lalu di bagian **Artifacts** unduh **SmartCBAnalyzer-apk** (file zip berisi `app-debug.apk`).
5. Kirim `app-debug.apk` ke HP Android dan pasang. Izinkan "pasang aplikasi dari sumber tidak dikenal".
   Jika muncul peringatan Play Protect, pilih **Tetap pasang**.

## Cara lain: Android Studio
(JDK 17 bawaan Studio sudah cukup)
1. Buka Android Studio, pilih **Open**, lalu pilih folder `SmartCBAnalyzerApp`.
2. Tunggu Gradle sync selesai (butuh internet, hanya untuk pertama kali).
3. Sambungkan HP (aktifkan USB debugging) lalu klik **Run**.
   Atau buat file APK: menu **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
   Hasil: `app/build/outputs/apk/debug/app-debug.apk`. Kirim ke HP dan pasang
   (izinkan "pasang aplikasi dari sumber tidak dikenal").

Lewat terminal (jika sudah punya Gradle): `gradle wrapper` sekali, lalu `./gradlew assembleDebug`.

## Pemakaian
1. Nyalakan alat (ESP32).
2. Buka aplikasi, tekan **Sambungkan otomatis**, setujui dialog sambungan WiFi dari Android.
3. Halaman pengujian terbuka. Ikuti langkah: Mode, Hitung mundur, Jalankan, Hasil.

Jika sambung otomatis gagal: sambungkan manual lewat **Buka pengaturan WiFi**
(pilih "Tetap terhubung" jika Android bilang WiFi tanpa internet), lalu tekan **Buka aplikasi**.

## Mengubah SSID / sandi
Jika `AP_SSID` atau `AP_PASS` di firmware diganti, ubah `SSID` dan `DEFAULT_PASS`
di bagian atas `MainActivity.kt` (sandi juga bisa diketik di layar sambung).

## Catatan
- Minimal Android 10 (API 29).
- iPhone: aplikasi ini tidak tersedia (butuh Mac + Xcode). Di iPhone, sambungkan ke WiFi alat
  lalu buka `http://192.168.4.1` di Safari.
