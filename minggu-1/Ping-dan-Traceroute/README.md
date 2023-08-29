# Ping dan Reaceroute

## 1. Ping

Ping merupakan singkatan dari Packet Internet Network Groper. Secara sederhana, ping adalah perintah untuk mengecek status dan keberadaan host dalam sebuah jaringan internet.

Prinsip utama ping adalah seperti penggunaan sonar untuk mengukur kedalaman laut. Jadi, sebuah sinyal dikirimkan ke dasar, lalu lamanya waktu kembali ke atas menjadi dasar perhitungannya.

### Cara kerja :

1. Komputer pengirim mengirimkan paket ICMP Echo Request ke host target dengan mengisi header dan payload yang sesuai. Host target menerima paket dan memprosesnya. Host target merespons dengan mengirimkan paket ICMP Echo Reply ke komputer pengirim. Komputer pengirim menerima balasan dan menghitung waktu yang diperlukan untuk paket pergi dan kembali. Waktu ini disebut sebagai "round-trip time" (RTT).
2. Host target menerima paket dan memprosesnya.
3. Komputer pengirim menerima balasan dan menghitung waktu yang diperlukan untuk paket pergi dan kembali.
4. Waktu ini disebut sebagai "round-trip time" (RTT).

<image src="./assets/cara-kerja-ping.png" alt="Open Systems Interconnection Illustration">

Di terminal atau command prompt, gunakan perintah "ping" untuk menjalankan tes ping. Berikut adalah contoh cara penggunaan perintah ping.

```
ping <alamat_IP_tujuan>
```

<alamat_IP_tujuan> adalah alamat IP dari perangkat yang ingin Anda uji koneksinya. Dibawah adalah contoh ping ke server google.co.id

<image src="./assets/contoh-ping.png" alt="Open Systems Interconnection Illustration">

## 2. Traceroute

Traceroute (Tracert) adalah perintah untuk menunjukkan rute yang dilewati paket untuk mencapai tujuan. Ini dilakukan dengan mengirim pesan Internet Control Message Protocol (ICMP) Echo Request Ke tujuan dengan nilai Time to Live yang semakin meningkat. Rute yang ditampilkan adalah daftar interface router (yang paling dekat dengan host) yang terdapat pada jalur antara host dan tujuan. Berikut adalah contohnya: 

<image src="./assets/contoh-traceroute.png" alt="Open Systems Interconnection Illustration">

### Cara kerja :
1. <strong>Mengirim Paket dengan TTL Berbeda:</strong> Ketika Anda menjalankan perintah traceroute ke suatu tujuan, perangkat Anda akan mengirim serangkaian paket data dengan Time-To-Live (TTL) yang berbeda. TTL adalah nilai numerik yang menunjukkan berapa banyak "hop" (router atau node jaringan) yang diizinkan untuk dilalui oleh paket sebelum paket tersebut dihapus dari jaringan. Setiap hop akan mengurangi nilai TTL paket sebelum melanjutkan pengiriman.
2. <strong>Menerima Respon dari Setiap Hop:</strong> Ketika paket mencapai setiap hop dalam perjalanannya, hop tersebut mengurangi nilai TTL paket tersebut dan kemudian mengirimkannya ke hop berikutnya. Jika TTL mencapai angka nol pada suatu hop, hop tersebut akan menghapus paket dan mengirimkan pesan kesalahan kembali kepada perangkat pengirim. Pesan kesalahan ini menunjukkan bahwa hop tersebut telah dijangkau dan juga memberikan informasi tentang hop tersebut.
3. <strong>Mengumpulkan Informasi Hop:</strong> Dalam setiap respon dari hop, perintah traceroute akan mencatat informasi seperti alamat IP hop tersebut, serta waktu yang dibutuhkan untuk paket pergi dari perangkat pengirim ke hop tersebut dan kembali lagi (round-trip time). Informasi ini digunakan untuk membangun gambaran jalur yang dilalui oleh paket data.
4. <strong>Menampilkan Hasil:</strong> Setelah traceroute selesai, hasilnya akan ditampilkan dalam bentuk daftar hop yang dilalui oleh paket, beserta informasi tentang alamat IP, round-trip time, dan nama host jika mungkin. Dengan informasi ini, Anda dapat melihat jalur yang diambil oleh paket data, melihat waktu tunda pada setiap hop, dan mengidentifikasi hop yang mungkin mengalami masalah atau mengakibatkan bottleneck.