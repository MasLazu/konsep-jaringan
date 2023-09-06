# Pemrograman Socket dalam Bahasa C: Server dan Klien Sederhana

`server.c` - server multithread

`server_single.c` - server singlethread

`client.c` - klien

## Pemrograman Socket

Ini adalah tutorial pra-proyek untuk pemrograman socket.

Jika Anda sudah familiar dengan pemrograman socket, silakan langsung menuju ke Bagian Praktik.

### 1. Apa Itu Socket?

* Dengan socket, dua proses yang berbeda dapat berkomunikasi satu sama lain.
* Socket hanyalah sebuah "file."
* Anda bisa membayangkan bahwa dua proses yang berbeda memiliki file (socket) dan mereka membaca data yang diterima dari socket dan menulis ke socket untuk mengirimkan data ke jaringan.
* Jadi, socket memiliki deskriptor file, yang hanyalah bilangan bulat untuk mengidentifikasi file yang terbuka.

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955905-363dae80-aef6-11e8-9719-ac759adbdfaa.png"/>
</p>

### 2. Jenis Socket

Ada dua jenis socket yang umum digunakan: "Socket Aliran" (Stream Sockets) dan "Socket Datagram" (Datagram Sockets). Socket aliran menggunakan TCP untuk transmisi data, sedangkan socket datagram menggunakan UDP.

### 3. Proses Klien & Proses Server

#### Klien: Biasanya meminta informasi dari server.

* Membuat socket dengan pemanggilan sistem `socket()`.
* Menghubungkan socket ke alamat server dengan pemanggilan sistem `connect()`.
* Mengirim dan menerima data. Ada beberapa cara untuk melakukannya, tetapi cara termudah adalah dengan menggunakan pemanggilan sistem `read()` dan `write()`.

#### Server: Menerima permintaan dari klien, melakukan pemrosesan yang diperlukan, dan mengirimkannya ke klien.

* Membuat socket dengan pemanggilan sistem `socket()`.
* Membinding socket ke alamat (IP + port) dengan pemanggilan sistem `bind()`.
* Mendengarkan koneksi dengan pemanggilan sistem `listen()`.
* Menerima koneksi dengan pemanggilan sistem `accept()`. Pemanggilan ini biasanya memblokir koneksi sampai seorang klien terhubung dengan server.
* Mengirim dan menerima data menggunakan pemanggilan sistem `read()` dan `write()`.

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955906-363dae80-aef6-11e8-9795-161a90f30b1e.png"/>
</p>

<p align="center">Interaksi antara server dan klien</p>

### Pengetahuan Pendahuluan Sebelum Memprogram

## 1. Struktur

Anda akan menggunakan fungsi-fungsi socket, dan sebagian besar fungsi socket menggunakan struktur alamat socket.

- `sockaddr`: struktur alamat socket generik

```objectivec
struct sockaddr {
    // mewakili famili alamat, dalam kebanyakan kasus AF_INET)
    unsigned short     sa_family;
    
    // 14 byte alamat spesifik protokol, untuk famili internet, nomor port dan alamat IP (sockaddr_in) digunakan
    char               sa_data[14]; 
}
```

- `sockaddr_in`: salah satu jenis sockaddr, ini mewakili nomor port dan alamat IP

```objectivec
struct sockaddr_in {
    short int              sin_family;   // AF_INET
    unsigned short int     sin_port;     // nomor port 16-bit
    struct in_addr         sin_addr;     // alamat IP 32-bit
    unsigned char          sin_zero[8];  
}
```

- `in_addr`: struktur yang digunakan dalam sockaddr_in

```objectivec
struct in_addr {
    unsigned long s_addr;
}
```

- `hostent`: mengandung informasi terkait host

```objectivec
struct hostent {
    char *h_name;       // contoh: unist.ac.kr
    char **h_aliases;   // daftar alias nama host
    int h_addrtype;     // AF_INET
    int h_length;       // panjang alamat IP 
    char **h_addr_list; // menunjuk ke struktur in_addr
    #define h_addr h_addr_list[0]
};
```

## 2. Urutan Byte Jaringan

Tidak semua komputer menyimpan byte dalam urutan yang sama. → Ada dua cara yang berbeda

- Little Endian: byte urutan rendah disimpan pada alamat awal
- Big Endian: byte urutan tinggi disimpan pada alamat awal

→ Untuk membuat mesin dengan urutan byte yang berbeda berkomunikasi satu sama lain, protokol Internet menentukan konvensi urutan byte kanonikal untuk data yang dikirimkan melalui jaringan. Ini disebut sebagai "Urutan Byte Jaringan."

`sin_port` dan `sin_addr` dari `sockaddr_in` harus diatur dengan Urutan Byte Jaringan ini.

```objectivec
htons(): Host ke Network Short
htonl(): Host ke Network Long
ntohl(): Network ke Host Long
ntohs(): Network ke Host Short
```

## 3. Fungsi Alamat IP

Fungsi-fungsi ini memanipulasi alamat IP antara string ASCII dan nilai biner berurutan byte jaringan.

- int `inet_aton`(const char *strptr, struct in_addr *addrptr)

```objectivec
#include <arpa/inet.h>
int retval;
struct in_addr addrptr
memset(&addrptr, '\0', sizeof(addrptr));
retval = inet_aton("68.178.157.132", &addrptr);
```

- in_addr_t `inet_addr`(const char *strptr)

```objectivec
#include <arpa/inet.h>
struct sockaddr_in dest;
memset(&dest, '\0', sizeof(dest));
dest.sin_addr.s_addr = inet_addr("68.178.157.132");
```

char `inet_ntoa`(struct in_addr inaddr)

```objectivec
#include <arpa/inet.h>
char *ip;
ip = inet_ntoa(dest.sin_addr);
printf("Alamat IP adalah: %s\n", ip);
```

## 4. Fungsi Socket

(Anda dapat menggunakan parameter yang dicetak tebal untuk penggunaan pertama)

1. `socket`

```objectivec
#include <sys/types.h>
#include <sys/socket.h>
int socket (int family, int type, int protocol);
```

- family: AF_INET, AF_INET6, AF_LOCAL, AF_ROUTE, AF_KEY
- type: SOCK_STREAM (TCP), SOCK_DGRAM (UDP), SOCK_SEQPACKET, SOCK_RAW
- protocol: IPPROTO_TCP

, IPPROTO_UDP, IPPROTO_SCTP, (0: default sistem)

→ Fungsi ini mengembalikan deskriptor socket, sehingga Anda dapat menggunakannya untuk fungsi lain.

2. `connect`

```objectivec
#include <sys/types.h>
#include <sys/socket.h>

int connect(int sockfd, struct sockaddr *serv_addr, int addrlen);
```

- sockfd: deskriptor socket yang dikembalikan oleh fungsi socket
- serv_addr: sockaddr yang berisi alamat IP dan port tujuan
- addrlen: atur ke sizeof(struct sockaddr)

3. `bind`

```objectivec
#include <sys/types.h>
#include <sys/socket.h>

int bind(int sockfd, struct sockaddr *my_addr, int addrlen);
```

- my_addr: sockaddr yang berisi alamat IP lokal dan port

4. `listen`

```objectivec
#include <sys/types.h>
#include <sys/socket.h>

int listen(int sockfd, int backlog);
```

- mengubah socket yang belum terhubung menjadi socket pasif (kernel harus menerima permintaan koneksi yang masuk yang ditujukan ke socket ini)
- backlog: jumlah maksimum koneksi yang harus diantrekan oleh kernel untuk socket ini

5. `accept`

```objectivec
#include <sys/types.h>
#include <sys/socket.h>

int accept (int sockfd, struct sockaddr *cliaddr, socklen_t *addrlen);
```

- mengembalikan koneksi yang telah selesai berikutnya dari depan antrian koneksi yang telah selesai
- cliaddr: struktur sockaddr yang berisi alamat IP dan port klien
- addrlen: atur ke sizeof(struct sockaddr)

5. `send`

```objectivec
int send(int sockfd, const void *msg, int len, int flags);
```

6. `recv`

```objectivec
int recv(int sockfd, void *buf, int len, unsigned int flags);
```
- buf: buffer untuk membaca informasi ke dalamnya
- len: ini adalah panjang maksimum buffer
- flags: atur ke 0

7. untuk koneksi UDP

```objectivec
int sendto(int sockfd, const void *msg, int len, unsigned int flags, const struct sockaddr *to, int tolen);
int recvfrom(int sockfd, void *buf, int len, unsigned int flags struct sockaddr *from, int *fromlen);
```
- `sendto` dan `recvfrom` digunakan alih-alih `send` `recv`

8. `close`

```objectivec
int close(int sockfd);
```

- menutup komunikasi
------
### 5. Fungsi Tambahan

1. `fork`

- Membuat proses baru yang merupakan salinan persis dari proses saat ini.
- Proses saat ini adalah induk, dan proses yang disalin adalah anak.

```objectivec
#include <sys/types.h>
#include <unistd.h>

int fork(void);
```

- `fork` mengembalikan 0 ketika itu adalah proses anak, dan mengembalikan ID proses anak ketika itu adalah proses induk. Jika gagal, mengembalikan -1.

2. `bzero`

- Menempatkan *n* byte byte null ke dalam string s.

```objectivec
void bzero(void *s, int nbyte);
```

3. `bcmp`

- Membandingkan *n* byte string byte s1 dan byte string s2.

```objectivec
int bcmp(const void *s1, const void *s2, int nbyte);
```

Mengembalikan 0 jika identik, 1 sebaliknya.

4. `bcopy`

- Menyalin *n* byte byte string s1 ke byte string s2.

```objectivec
void bcopy(const void *s1, void *s2, int nbyte);
```

5. `memset`

- Mengalokasikan memori dan mengembalikan pointer yang menunjuk ke memori yang baru dialokasikan.

```objectivec
void *memset(void *s, int c, int nbyte);
```

- s: sumber yang akan diatur
- c: karakter yang akan diatur pada nbyte tempat
- nbyte: jumlah byte

## 6. Mari Berlatih: Server dan Klien Echo

- Anda harus mengimplementasikan koneksi server dan klien,
dan server dan klien Anda harus berhenti ketika klien mengirimkan "quit"
Anda dapat mengompilasi kode dengan baris perintah dalam direktori proyek:

```
> make
```

- Jalankan server dan klien di server pada saat yang sama
- dengan dua jendela terminal yang berbeda

```
> ./client
> ./server
```

- Keluaran Contoh

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955907-36d64500-aef6-11e8-886e-1fcf77b377c4.png"/>
</p>

<p align="center">klien</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955908-36d64500-aef6-11e8-9888-ab63856ad2d4.png"/>
</p>

<p align="center">server</p>

## 7. Latihan Lebih Banyak: Server Multi Pengguna

- Bisa ada beberapa klien yang mencoba menghubungkan diri ke server secara bersamaan
- Server echo saat ini tidak menerima koneksi baru jika sudah diterima
- Anda harus mengubah server echo. Dengan menggunakan fungsi `fork()`, setiap koneksi harus dijalankan secara bersamaan.
- Petunjuk (kode semu server multi pengguna):

```
listen()
while (1) {
    newsockfd = accept();
    pid = fork();
    if (pid == 0) { // proses klien
        close(sockfd);
        // melakukan beberapa proses - membaca dan menulis
        exit(0);
    } else { // proses induk
        close(newsockfd);
    }
}
```

- Uji: Anda hanya perlu membuka tiga jendela terminal, menjalankan satu server dan dua klien
- urutan pengujian:

```
> jalankan satu server dan dua klien
> klien1 mengirim "hello1"
> klien2 mengirim "hello2"
> klien2 mengirim "world2"
> klien1 mengirim "world1"
> klien1 mengirim "quit" dan klien2 mengirim "quit"
```

Keluaran:

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955909-36d64500-aef6-11e8-9345-1033eb29599c.png"/>
</p>

<p align="center">klien1</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955910-36d64500-aef6-11e8-8f04-3a7a2deb1b6f.png"/>
</p>

<p align="center">klien2</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/19291492/44955911-376edb80-aef6-11e8-929e-56667b372253.png"/>
</p>

<p align="center">server multi pengguna</p>