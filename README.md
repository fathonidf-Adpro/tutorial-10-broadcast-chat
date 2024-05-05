# TUTORIAL 10 ADPRO  (Asynchronous Programming)
#### Daffa Mohamad Fathoni (2206824161)
#### Advanced Programming B / GEN

<hr>

## REFLECTION
>Experiment 2.1: Original code, and how it run

![image](https://github.com/fathonidf-Adpro/tutorial-10-timer/assets/105644250/d33c3571-2782-4711-8d9e-8b2e63891d0f)

Cara menjalankannya sebagai berikut:
1. **Pengaturan Server**:
- Mulai server dengan menggunakan perintah `cargo run --bin server` dari terminal.

2. **Pengaturan Klien**:
- Buka tiga terminal berbeda.
- Jalankan perintah `cargo run --bin client` di setiap terminal untuk memulai tiga klien.

3. **Proses Pengiriman Pesan**:
- Setiap klien yang mengetik pesan dan mengirimkannya akan mengirimkan pesan tersebut ke server.
- Server kemudian menerima pesan tersebut dan meneruskannya ke setiap klien yang terhubung.
- Akibatnya, setiap pesan yang dikirim oleh klien akan diterima oleh semua klien lain yang terhubung ke server melalui proses broadcast.