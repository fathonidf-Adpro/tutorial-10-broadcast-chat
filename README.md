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

>Experiment 2.2: Modifying port

![image](https://github.com/fathonidf-Adpro/tutorial-10-broadcast-chat/assets/105644250/19c0a106-33d7-43b2-b1a4-a1bb50f75085)

untuk mengganti port menjadi `8080`, maka saya mengubah file yang ada pada `server.rs` sebagai berikut:
```rust
#[tokio::main]
async fn main() -> Result<(), Box<dyn Error + Send + Sync>> {
    let (bcast_tx, _) = channel(16);

    let listener = TcpListener::bind("127.0.0.1:8080").await?;
    println!("listening on port 8080");

    ...
}
```

Dan juga pada `client.rs` sebagai berikut:
```rust
#[tokio::main]
async fn main() -> Result<(), tokio_websockets::Error> {
    let (mut ws_stream, _) =
        ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
            .connect()
            .await?;
}
```

Karena pada sisi client dan server sama-sama memiliki port yang sama, maka program akan tetap berjalan dengan lancar seperti gambar di atas.

Namun, jika terdapat port yang berbeda pada client (pada client menjadi port 2000 sementara server menjadi port 8080). Maka akan muncul error sebagai berikut di terminal

```
Error: Io(Os { code: 10061, kind: ConnectionRefused, message: "No connection could be made because the target machine actively refused it." })
error: process didn't exit successfully: `target\debug\client.exe` (exit code: 1)
```
Dan seperti gambar berikut:
![image](https://github.com/fathonidf-Adpro/tutorial-10-broadcast-chat/assets/105644250/096c4b64-f1df-4e9a-a57c-e058dda85148)

Error terjadi karena klien mencoba terhubung ke port 8080 sedangkan server yang dijalankan mendengarkan pada port 2020, sehingga tidak ada server yang aktif di port yang dicoba klien untuk terhubung.