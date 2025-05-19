# Tutorial 10 Advance Programming
Muhammad Albyarto Ghazali (2306241695)

### 2.1. Original code of broadcast chat

**Screen Capture (one server, and three clients):**
![alt text](image.png)

Aplikasi ini merupakan simulasi sederhana dari sistem **chat real-time** berbasis **WebSocket** menggunakan library `tokio` dan `tokio-websockets`. Aplikasi terdiri dari dua komponen utama, server dan client. Server berfungsi sebagai pusat komunikasi yang menerima koneksi dari berbagai client dan meneruskan message dari satu client ke seluruh client lainnya. Sementara itu, client dapat mengirim message ke server dan menerima message dari client lain melalui server.

Untuk menjalankan aplikasi ini, langkah pertama yang harus dilakukan adalah menjalankan **server**. Buka terminal dan jalankan perintah `cargo run --bin server`. Server akan berjalan dan mendengarkan koneksi di alamat `127.0.0.1` port `2000`. Setelah server aktif, buka tiga terminal baru secara terpisah dan jalankan program **client** di masing-masing terminal menggunakan perintah `cargo run --bin client`. Dengan ini, akan ada tiga client yang aktif dan terhubung ke server.

Setiap client yang baru terhubung akan menerima message sambutan dari server: *"Welcome to chat! Type a message"*. Selanjutnya, pengguna dapat langsung mengetik message di terminal dan menekan Enter untuk mengirimkan message tersebut ke server. Setelah message dikirim, server akan menyebarkan (broadcast) message tersebut ke semua client yang terhubung, termasuk pengirimnya sendiri. Akibatnya, setiap client akan melihat message yang dikirim oleh client lain dalam waktu nyata. Misalnya, jika client pertama mengirimkan message “Halo semua!”, maka message tersebut akan langsung muncul juga di terminal client kedua dan ketiga. Begitu juga saat client lain mengirimkan message, seluruh peserta akan langsung menerimanya.

Semua proses komunikasi ini berjalan secara **asynchronous dan parallel** karena penggunaan `tokio::select!`, yang memungkinkan client handle input dari pengguna dan menerima message dari server secara bersamaan. Sistem ini mencerminkan bagaimana aplikasi chat modern bekerja di balik layar—dengan saling bertukar message melalui server menggunakan koneksi **WebSocket** yang stabil dan terus-menerus aktif.

---
