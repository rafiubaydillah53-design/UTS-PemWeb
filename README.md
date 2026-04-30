# UTS-PemWeb
SQL INJECTION

1. Mekanisme Serangan SQL Injection
SQL Injection (SQLi) adalah teknik serangan di mana penyerang menyisipkan perintah SQL berbahaya ke dalam kolom input aplikasi untuk memanipulasi kueri database.

Dalam eksperimen ini, saya menggunakan skrip login_vulnerable.php. Kueri yang digunakan pada skrip tersebut adalah:
$sql = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";

Ketika saya memasukkan payload ' OR 1=1 # pada kolom username, database menerima instruksi yang berubah menjadi:
SELECT * FROM users WHERE username = '' OR 1=1 # AND password = '...'

Tanda petik (') menutup field username secara prematur.

Perintah OR 1=1 menciptakan kondisi yang selalu bernilai TRUE, sehingga sistem dipaksa menganggap input tersebut benar tanpa memeriksa kata sandi.

Simbol # berfungsi sebagai operator komentar di MySQL, yang memerintahkan database untuk mengabaikan sisa perintah setelahnya (termasuk pengecekan password).

2. Hasil Eksperimen
Berdasarkan pengujian, sistem yang rentan berhasil ditembus dan memberikan pesan "Login Berhasil!" meskipun password yang dimasukkan salah. Hal ini membuktikan bahwa validasi input sangat krusial dalam keamanan web.

3. Implementasi Mitigasi dengan Prepared Statements
Untuk mengatasi kerentanan ini, saya mengimplementasikan Prepared Statements pada skrip login_secure.php. Teknik ini bekerja dengan cara memisahkan struktur kueri dari data input.

PHP
// Kode Mitigasi (Prepared Statement)
$stmt = $conn->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->bind_param("ss", $username, $password);
$stmt->execute();
Dengan cara ini, input penyerang seperti ' OR 1=1 # tidak lagi dianggap sebagai perintah SQL, melainkan hanya dianggap sebagai sebuah string teks biasa yang dicari di dalam database. Hasilnya, sistem tetap menolak akses karena tidak ditemukan user dengan username yang mengandung karakter tersebut.

