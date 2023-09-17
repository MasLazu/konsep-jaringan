# TELNET

## 1. PENGERTIAN

Telnet adalah sebuah protokol jaringan yang digunakan untuk mengakses dan mengendalikan perangkat jarak jauh melalui jaringan komputer. Protokol ini memungkinkan pengguna untuk melakukan akses jarak jauh ke perangkat seperti server, router, atau komputer lainnya, seolah-olah mereka sedang duduk di depan perangkat tersebut secara fisik. Telnet menggunakan koneksi TCP/IP (Transmission Control Protocol/Internet Protocol) untuk mentransmisikan data antara komputer pengguna (client) dan komputer tujuan (server) melalui jaringan.

# 2. RFC

Telnet didokumentasikan dalam beberapa RFC. RFC adalah serangkaian dokumen yang digunakan untuk menggambarkan protokol dan standar di internet. Telnet awalnya dijelaskan dalam RFC 854, yang kemudian diperbarui oleh RFC 855, RFC 856, dan RFC 857. RFC terbaru yang terkait dengan Telnet adalah RFC 854, yang diterbitkan pada tahun 1983. Namun, penggunaan Telnet telah menurun seiring waktu karena kurangnya keamanan, dan protokol pengganti yang lebih aman seperti SSH telah menjadi lebih populer.

## 3. TCP FLOW GRAPH

Telnet adalah protokol jaringan yang berbasis TCP (Transmission Control Protocol), sehingga alur atau "flow" dari koneksi Telnet mengikuti model dasar yang sama dengan alur koneksi TCP pada umumnya. Di bawah ini, saya akan menjelaskan bagaimana alur koneksi Telnet TCP berlangsung dalam bentuk grafik alur:

<div align="center">
<img src="./assets/telnet-tcp-flow-graph.png">

1.1 telnet tcp flow graph

</div>

1. Pengguna memulai koneksi Telnet dengan mengirimkan permintaan koneksi (SYN) ke server Telnet.
2. Klien Telnet mengirimkan data ke server, seperti permintaan autentikasi (nama pengguna dan kata sandi).
3. Server Telnet menerima data dan memprosesnya, kemungkinan dengan meminta pengguna untuk memasukkan informasi autentikasi.
4. Server Telnet membalas dengan mengirimkan data balasan.
5. Klien Telnet menerima data balasan dari server.
6. Klien Telnet mengirimkan lebih banyak data atau perintah ke server (interaksi berlanjut).
7. Server Telnet menerima perintah dari klien dan merespons dengan mengirimkan data lebih lanjut.
8. Pengguna mengirimkan permintaan untuk menutup koneksi (FIN) ke server setelah selesai.
9. Server Telnet merespons dengan mengirimkan konfirmasi penutupan koneksi (FIN), dan koneksi ditutup.

### 4. KARAKTERISTIK

Telnet memiliki beberapa karakteristik utama Telnet meliputi:

1. **Koneksi Teks:** Telnet adalah protokol berbasis teks, yang berarti data yang dikirimkan antara client dan server berbentuk teks biasa. Ini berbeda dengan protokol seperti SSH (Secure Shell) yang memiliki tingkat keamanan yang lebih tinggi dan mendukung enkripsi, sementara Telnet tidak.
   
2. **Port Standar:** Port standar yang digunakan oleh Telnet adalah 23. Untuk melakukan koneksi Telnet, Anda perlu mengetahui alamat IP atau nama host tujuan, serta nomor port jika berbeda dari 23.

3. **Kurang Aman:** Salah satu karakteristik utama Telnet adalah kurangnya keamanan. Data yang dikirimkan melalui Telnet tidak dienkripsi, yang berarti informasi seperti nama pengguna dan kata sandi dapat dengan mudah diintersep oleh pihak yang tidak berwenang jika mereka memiliki akses ke jaringan yang digunakan.
   
4. **Interoperabilitas:** Salah satu keunggulan Telnet adalah interoperabilitasnya yang tinggi. Banyak perangkat jaringan dan sistem operasi yang mendukung Telnet, sehingga pengguna dapat dengan mudah terhubung ke berbagai jenis perangkat dari berbagai vendor menggunakan Telnet.

Meskipun Telnet masih digunakan dalam beberapa kasus, seperti konfigurasi perangkat jaringan khusus yang tidak memiliki alternatif yang lebih aman, sebaiknya dihindari penggunaan Telnet dalam situasi di mana keamanan informasi sangat penting. Sebagai gantinya, disarankan untuk menggunakan protokol yang lebih aman seperti SSH.