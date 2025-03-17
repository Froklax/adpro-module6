# Reflection Module 6 - Concurrency

## Commit 1 Reflection notes
Fungsi `handle_connection` dalam file `main.rs` bertugas untuk menampilkan _raw HTTP request_ yang dikirimkan ke server. Dalam prosesnya, fungsi ini menerima sebuah `TcpStream` yang bersifat _mutable_ dan kemudian memberikan referensinya ke dalam `BufReader`. `BufReader` membaca aliran data dengan memecah input berdasarkan karakter _newline_ atau CRLF, lalu mengembalikan setiap baris dalam bentuk `Result<String, Error>`. Setiap hasil tersebut di-_unwrapping_ dan diambil nilainya, dengan proses diiterasikan sampai ditemukan baris kosong yang menandai akhir dari bagian _header request_. Data yang diperoleh kemudian dikumpulkan dalam sebuah _vector_ `Vec<_>`, yang kemudian ditampilkan ke layar untuk menunjukkan bagaimana request tersebut disusun oleh browser.

## Commit 2 Reflection notes
Fungsi `handle_connection` yang dimodifikasi mengirimkan _HTTP response_ dengan status `200 OK` dan memuat konten `HTML` yang diambil dari file `hello.html`. File tersebut dibaca menggunakan `fs::read_to_string` untuk mendapatkan konten dalam bentuk string, kemudian panjang konten dihitung dan dimasukkan ke dalam header `Content-Length`. Header `Content-Length` memberikan informasi kepada browser mengenai ukuran data yang dikirim, sehingga browser dapat menampilkan halaman secara utuh. _Response_ diformat sesuai standar HTTP, dimulai dengan _status line_, dilanjutkan header, kemudian baris kosong, dan diakhiri dengan _body_ yang berisi `HTML`. Setelah itu, _response_ dikirim ke _client_ menggunakan `stream.write_all()`.

_Screenshot_ hasil menjalankan modifikasi kode terbaru:
![Commit 2 screen capture](./commit2.png)