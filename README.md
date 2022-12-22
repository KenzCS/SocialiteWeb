# SocialiteWeb

1. Instal paket Socialite ke dalam aplikasi Laravel Anda menggunakan Composer:
    ``` komposer memerlukan laravel/sosialita```
2. Tambahkan penyedia layanan Socialite ke file `config/app.php` Anda di array provider:
    ```Laravel\Socialite\SocialiteServiceProvider::class,```
3. Daftarkan aplikasi ke Google dan dapatkan ID Klien dan kunci rahasia dengan mengunjungi Google Developers Console (https://console.developers.google.com). Setelah Anda mendaftarkan aplikasi, pastikan Anda menambahkan http://example.com/login/google sebagai salah satu URI pengalihan resmi Anda untuk alasan keamanan agar hanya mengizinkan permintaan resmi.
4. Tambahkan kredensial ke file `config/services.php` Anda:
     ``` 'google' => [
         'client_id' => 'id-aplikasi-Anda',
         'client_secret' => 'rahasia-aplikasi-Anda',
         'redirect' => '/login/google/callback', // atau apa pun yang Anda inginkan, pastikan cocok dengan apa yang diatur di konsol Google
     ]```
5. Buat rute untuk mengalihkan pengguna ke halaman autentikasi Google:
    ```Rute::get('login/google', 'Auth\LoginController@redirectToProvider');```
6. Buat pengontrol dengan metode yang akan menangani panggilan balik dari Google setelah pengguna mengautentikasi:
    ```fungsi publik handleProviderCallback() {
         $user = Socialite::driver('google')->user();

         // sekarang Anda dapat menggunakan objek $user untuk menemukan atau membuat pengguna baru di database Anda, dll..

         kembali redirect('/rumah'); }```
7. Tambahkan rute lain ke `web.php` Anda, kali ini untuk menangani callback dari Google:
    ```Rute::get('login/google/callback', 'Auth\LoginController@handleProviderCallback');```
8. Terakhir, Anda sekarang dapat menggunakan fasad Sosialita untuk mengautentikasi pengguna menggunakan Google:
    ```Sosialita::driver('google')->redirect();```
