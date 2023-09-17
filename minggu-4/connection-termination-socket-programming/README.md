# CONNECTION TERMINATION SOCKET PROGRAMMING

## 1. quit

Ketika mengetikkan "quit" di terminal client (client.c), koneksi akan ditutup sepenuhnya (full closed).

Pada kode client terdapat code berikut:
```
if (!bcmp(buffer, "quit", 4))
    break;
```
Ini berarti jika server mengirimkan pesan "quit" kepada client, maka client akan keluar dari loop dan mengakhiri program. Dengan demikian, client akan menutup koneksi ke server secara penuh (full closed) ketika kondisi ini terpenuhi, dan tidak akan mengirim atau menerima data lagi setelah itu.

Jadi, koneksi akan ditutup sepenuhnya (full closed) setelah client menerima pesan "quit" dari server.

## 2. close

Ketika mengetikkan "close" di terminal client (client.c), koneksi akan ditutup secara setengah (half closed) dari sisi client.

Pada client, terdapat code berikut:
```
scanf("%s", buffer);
```

Ini berarti cliet akan membaca input dari pengguna dan menempatkannya dalam buffer. Jika mengetikkan "close" dan mengirimkannya ke server, cliet akan mengirim "close" ke server melalui koneksi, tetapi koneksi itu sendiri tidak akan ditutup sepenuhnya oleh cliet. Ini berarti cliet masih dapat menerima data dari server setelah mengirim "close", tetapi tidak dapat lagi mengirimkan data ke server.

Namun, dalam kode server, ada potongan kode yang mengarah ke penutupan koneksi dari sisi server jika pesan yang diterima adalah "close". Kode berikut di server.c:

```
if (buffer == "close") {
    printf("Process %d: ", getpid());
    close(client_fd);
    printf("Closing session with `%d`. Bye!\n", client_fd);
    break;
}
```

Jadi, jika server mendeteksi pesan "close" dari client, server akan menutup koneksi ke client, sehingga koneksi akan menjadi setengah (half closed) dari sisi server. Koneksi akan tetap terbuka dari sisi client hingga client juga menutupnya secara eksplisit atau hingga terjadi kesalahan pada koneksi.

Jadi, dengan kata lain, jika Anda mengetikkan "close" di client, koneksi akan menjadi setengah tertutup (half closed) dari sisi server dan tetap terbuka dari sisi client sampai client juga menutupnya atau terjadi kesalahan.