# TRACE ROUTE

## 1.1.1.1

<div align="center">
<img src="assets/1.1.1.1.jpg">
</div>

### Percobaan pertama
- **Hasil :**
    ```
    student@localhost:~$ traceroute 1.1.1.1
    traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.830 ms  0.780 ms  0.741 ms
    2  10.252.108.212 (10.252.108.212)  0.703 ms  0.697 ms  0.662 ms
    3  241.56.pens.ac.id (103.24.56.241)  6.033 ms * *
    4  core-router.pens.ac.id (202.9.85.1)  1.675 ms  1.726 ms  2.090 ms
    5  edge-router.pens.ac.id (10.252.0.1)  1.519 ms  1.468 ms  1.503 ms
    6  114-4-97-169.resources.indosat.com (114.4.97.169)  2.691 ms  2.344 ms  2.271 ms
    7  114-0-78-196.resources.indosat.com (114.0.78.196)  24.056 ms  23.976 ms  23.925 ms
    8  * * *
    9  * * *
    10  * * *
    11  * * one.one.one.one (1.1.1.1)  24.743 ms

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1. Ini kemungkinan besar adalah router atau modem di kampus.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212.

    Baris 3: Hop ketiga ke alamat IP 103.24.56.241, yang tampaknya terkait dengan pens.ac.id.

    Baris 4: Hop keempat ke alamat IP 202.9.85.1, yang sepertinya merupakan router inti di pens.ac.id.

    Baris 5: Hop kelima ke alamat IP 10.252.0.1, yang tampaknya merupakan router tepi di pens.ac.id.

    Baris 6: Hop keenam ke alamat IP 114.4.97.169, yang merupakan bagian dari sumber daya indosat.com.

    Baris 7: Hop ketujuh ke alamat IP 114.0.78.196, sumber daya indosat.com lainnya.

    Baris 8-10: Baris ini menunjukkan bahwa traceroute tidak menerima tanggapan untuk hop kedelapan hingga kesepuluh.

    Baris 11: Hop kesebelas berhasil mencapai alamat IP tujuan 1.1.1.1, yang merupakan resolver DNS Cloudflare.

### Percobaan kedua
- **Hasil :**
    ```
    student@localhost:~$ traceroute 1.1.1.1
    traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.214 ms  0.133 ms  0.158 ms
    2  10.252.108.212 (10.252.108.212)  0.264 ms  0.209 ms  0.238 ms
    3  241.56.pens.ac.id (103.24.56.241)  0.432 ms * *
    4  core-router.pens.ac.id (202.9.85.1)  1.347 ms  1.459 ms  1.591 ms
    5  edge-router.pens.ac.id (10.252.0.1)  1.095 ms  1.045 ms  1.011 ms
    6  114-4-97-169.resources.indosat.com (114.4.97.169)  2.374 ms  2.586 ms  2.520 ms
    7  114-0-78-196.resources.indosat.com (114.0.78.196)  24.027 ms  22.922 ms  24.875 ms
    8  * * 13335.sgw.equinix.com (27.111.228.132)  23.593 ms
    9  * 172.70.140.3 (172.70.140.3)  25.441 ms *
    10  one.one.one.one (1.1.1.1)  24.978 ms  24.930 ms  24.629 ms

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1. Waktu yang tercantum (0.214 ms, 0.133 ms, 0.158 ms) menunjukkan waktu tempuh paket dari komputer ke gateway tersebut dan kembali.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212. Waktu tempuhnya adalah 0.264 ms, 0.209 ms, dan 0.238 ms.

    Baris 3: Hop ketiga ke alamat IP 103.24.56.241 (241.56.pens.ac.id). Waktu tempuh pertama adalah 0.432 ms, dan dua kali setelahnya tidak mendapatkan respons (ditandai dengan "*"). Ini mungkin disebabkan oleh konfigurasi jaringan yang tidak mengizinkan respons terhadap permintaan ICMP.

    Baris 4: Hop keempat ke alamat IP 202.9.85.1 (core-router.pens.ac.id) dengan waktu tempuh 1.347 ms, 1.459 ms, dan 1.591 ms.

    Baris 5: Hop kelima ke alamat IP 10.252.0.1 (edge-router.pens.ac.id) dengan waktu tempuh 1.095 ms, 1.045 ms, dan 1.011 ms.

    Baris 6: Hop keenam ke alamat IP 114.4.97.169 (114-4-97-169.resources.indosat.com) dengan waktu tempuh 2.374 ms, 2.586 ms, dan 2.520 ms.

    Baris 7: Hop ketujuh ke alamat IP 114.0.78.196 (114-0-78-196.resources.indosat.com) dengan waktu tempuh 24.027 ms, 22.922 ms, dan 24.875 ms.

    Baris 8: Hop kedelapan tidak memberikan respons (ditandai dengan "*"). Alamat IP berikutnya adalah 13335.sgw.equinix.com (27.111.228.132) dengan waktu tempuh 23.593 ms.

    Baris 9: Hop kesembilan dengan alamat IP 172.70.140.3, waktu tempuh 25.441 ms, dan satu kali tidak mendapatkan respons.

    Baris 10: Hop kesepuluh mencapai tujuan dengan alamat IP 1.1.1.1 (one.one.one.one) dengan waktu tempuh 24.978 ms, 24.930 ms, dan 24.629 ms.

### Percobaan ketiga
- **Hasil :**
    ```
    student@localhost:~$ traceroute 1.1.1.1
    traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.207 ms  0.132 ms  0.083 ms
    2  10.252.108.212 (10.252.108.212)  0.267 ms  0.219 ms  0.174 ms
    3  * * *
    4  core-router.pens.ac.id (202.9.85.1)  0.885 ms  0.992 ms  1.055 ms
    5  edge-router.pens.ac.id (10.252.0.1)  1.277 ms  1.319 ms  1.274 ms
    6  114-4-97-169.resources.indosat.com (114.4.97.169)  2.377 ms  2.307 ms  2.244 ms
    7  114-0-78-196.resources.indosat.com (114.0.78.196)  23.122 ms  23.223 ms  23.031 ms
    8  * * *
    9  162.158.168.2 (162.158.168.2)  25.983 ms 162.158.104.3 (162.158.104.3)  29.785 ms *
    10  one.one.one.one (1.1.1.1)  24.194 ms  24.565 ms *

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1, dengan waktu tempuh masing-masing 0.207 ms, 0.132 ms, dan 0.083 ms.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212, dengan waktu tempuh masing-masing 0.267 ms, 0.219 ms, dan 0.174 ms.

    Baris 3: Hop ketiga tidak memberikan respons (ditandai dengan "*"). Ini mungkin disebabkan oleh konfigurasi jaringan yang tidak mengizinkan respons terhadap permintaan ICMP.

    Baris 4: Hop keempat menuju core-router.pens.ac.id dengan alamat IP 202.9.85.1, dengan waktu tempuh masing-masing 0.885 ms, 0.992 ms, dan 1.055 ms.

    Baris 5: Hop kelima menuju edge-router.pens.ac.id dengan alamat IP 10.252.0.1, dengan waktu tempuh masing-masing 1.277 ms, 1.319 ms, dan 1.274 ms.

    Baris 6: Hop keenam menuju 114-4-97-169.resources.indosat.com dengan alamat IP 114.4.97.169, dengan waktu tempuh masing-masing 2.377 ms, 2.307 ms, dan 2.244 ms.

    Baris 7: Hop ketujuh menuju 114-0-78-196.resources.indosat.com dengan alamat IP 114.0.78.196, dengan waktu tempuh masing-masing 23.122 ms, 23.223 ms, dan 23.031 ms.

    Baris 8: Hop kedelapan tidak memberikan respons (ditandai dengan "*").

    Baris 9: Hop kesembilan menuju alamat IP 162.158.168.2 dan 162.158.104.3, dengan waktu tempuh masing-masing 25.983 ms dan 29.785 ms.

    Baris 10: Hop kesepuluh mencapai tujuan dengan alamat IP 1.1.1.1 (one.one.one.one) dengan waktu tempuh masing-masing 24.194 ms, 24.565 ms, dan satu kali tidak mendapatkan respons.

## detik.com

<div align="center">
<img src="assets/detik.com.jpg">
</div>

### Percobaan pertama
- **Hasil :**
    ```
    student@localhost:~$ traceroute detik.com
    traceroute to detik.com (103.49.221.211), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.195 ms  0.102 ms  0.142 ms
    2  10.252.108.212 (10.252.108.212)  0.254 ms  0.181 ms  0.216 ms
    3  * * *
    4  core-router.pens.ac.id (202.9.85.1)  1.158 ms  1.104 ms  1.051 ms
    5  edge-router.pens.ac.id (10.252.0.1)  0.998 ms  0.944 ms  1.136 ms
    6  124-195-38-7.resources.indosat.com (124.195.38.7)  13.198 ms  12.450 ms  12.374 ms
    7  123.108.8.172 (123.108.8.172)  12.968 ms  14.207 ms  14.122 ms
    8  * * *
    9  * * *
    10  * * *
    11  * * *
    12  * s211-cast-211-221-49-103.detik.com (103.49.221.211)  13.730 ms *

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1, dengan waktu tempuh masing-masing 0.195 ms, 0.102 ms, dan 0.142 ms.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212, dengan waktu tempuh masing-masing 0.254 ms, 0.181 ms, dan 0.216 ms.

    Baris 3: Hop ketiga tidak memberikan respons (ditandai dengan "*"). Ini mungkin disebabkan oleh konfigurasi jaringan yang tidak mengizinkan respons terhadap permintaan ICMP.

    Baris 4: Hop keempat menuju core-router.pens.ac.id dengan alamat IP 202.9.85.1, dengan waktu tempuh masing-masing 1.158 ms, 1.104 ms, dan 1.051 ms.

    Baris 5: Hop kelima menuju edge-router.pens.ac.id dengan alamat IP 10.252.0.1, dengan waktu tempuh masing-masing 0.998 ms, 0.944 ms, dan 1.136 ms.

    Baris 6: Hop keenam menuju 124-195-38-7.resources.indosat.com dengan alamat IP 124.195.38.7, dengan waktu tempuh masing-masing 13.198 ms, 12.450 ms, dan 12.374 ms.

    Baris 7: Hop ketujuh menuju 123.108.8.172 dengan alamat IP 123.108.8.172, dengan waktu tempuh masing-masing 12.968 ms, 14.207 ms, dan 14.122 ms.

    Baris 8-11: Hop kedelapan hingga kesebelas tidak memberikan respons (ditandai dengan "*").

    Baris 12: Hop keduabelas mencapai tujuan dengan alamat IP 103.49.221.211 (s211-cast-211-221-49-103.detik.com) dengan waktu tempuh 13.730 ms, dan satu kali tidak mendapatkan respons.

### Percobaan kedua
- **Hasil :**
    ```
    student@localhost:~$ traceroute detik.com
    traceroute to detik.com (203.190.242.211), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.192 ms  0.126 ms  0.076 ms
    2  10.252.108.212 (10.252.108.212)  0.261 ms  0.212 ms  0.242 ms
    3  * * *
    4  core-router.pens.ac.id (202.9.85.1)  0.858 ms  1.013 ms  0.962 ms
    5  edge-router.pens.ac.id (10.252.0.1)  0.876 ms  0.829 ms  0.906 ms
    6  124-195-39-3.resources.indosat.com (124.195.39.3)  13.347 ms  13.799 ms  14.495 ms
    7  * * *
    8  218.100.36.9 (218.100.36.9)  14.020 ms  13.873 ms  14.357 ms
    9  s2-211-242.190.203.detik.com (203.190.242.211)  13.299 ms  13.262 ms  13.205 ms

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1, dengan waktu tempuh masing-masing 0.192 ms, 0.126 ms, dan 0.076 ms.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212, dengan waktu tempuh masing-masing 0.261 ms, 0.212 ms, dan 0.242 ms.

    Baris 3: Hop ketiga tidak memberikan respons (ditandai dengan "*"). Ini mungkin disebabkan oleh konfigurasi jaringan yang tidak mengizinkan respons terhadap permintaan ICMP.

    Baris 4: Hop keempat menuju core-router.pens.ac.id dengan alamat IP 202.9.85.1, dengan waktu tempuh masing-masing 0.858 ms, 1.013 ms, dan 0.962 ms.

    Baris 5: Hop kelima menuju edge-router.pens.ac.id dengan alamat IP 10.252.0.1, dengan waktu tempuh masing-masing 0.876 ms, 0.829 ms, dan 0.906 ms.

    Baris 6: Hop keenam menuju 124-195-39-3.resources.indosat.com dengan alamat IP 124.195.39.3, dengan waktu tempuh masing-masing 13.347 ms, 13.799 ms, dan 14.495 ms.

    Baris 7: Hop ketujuh tidak memberikan respons (ditandai dengan "*").

    Baris 8: Hop kedelapan menuju 218.100.36.9 dengan alamat IP 218.100.36.9, dengan waktu tempuh masing-masing 14.020 ms, 13.873 ms, dan 14.357 ms.

    Baris 9: Hop kesembilan mencapai tujuan dengan alamat IP 203.190.242.211 (s2-211-242.190.203.detik.com) dengan waktu tempuh masing-masing 13.299 ms, 13.262 ms, dan 13.205 ms.

### Percobaan ketiga
- **Hasil :**
    ```
    student@localhost:~$ traceroute detik.com
    traceroute to detik.com (103.49.221.211), 30 hops max, 60 byte packets
    1  _gateway (192.168.6.1)  0.208 ms  0.133 ms  0.151 ms
    2  10.252.108.212 (10.252.108.212)  0.252 ms  0.202 ms  0.275 ms
    3  241.56.pens.ac.id (103.24.56.241)  0.428 ms * *
    4  core-router.pens.ac.id (202.9.85.1)  0.991 ms  1.046 ms  1.054 ms
    5  edge-router.pens.ac.id (10.252.0.1)  0.952 ms  0.906 ms  0.914 ms
    6  124-195-38-7.resources.indosat.com (124.195.38.7)  11.808 ms  12.077 ms  11.886 ms
    7  123.108.8.172 (123.108.8.172)  14.260 ms  14.813 ms  14.763 ms
    8  s211-cast-211-221-49-103.detik.com (103.49.221.211)  12.068 ms  12.020 ms *

    ```
- **Penjelasan :**
    
    Baris 1: Gateway lokal dengan alamat IP 192.168.6.1, dengan waktu tempuh masing-masing 0.208 ms, 0.133 ms, dan 0.151 ms.

    Baris 2: Hop kedua ke alamat IP 10.252.108.212, dengan waktu tempuh masing-masing 0.252 ms, 0.202 ms, dan 0.275 ms.

    Baris 3: Hop ketiga menuju 241.56.pens.ac.id dengan alamat IP 103.24.56.241, dengan waktu tempuh 0.428 ms. Dua kali setelahnya tidak mendapatkan respons (ditandai dengan "*"). Ini mungkin disebabkan oleh konfigurasi jaringan yang tidak mengizinkan respons terhadap permintaan ICMP.

    Baris 4: Hop keempat menuju core-router.pens.ac.id dengan alamat IP 202.9.85.1, dengan waktu tempuh masing-masing 0.991 ms, 1.046 ms, dan 1.054 ms.

    Baris 5: Hop kelima menuju edge-router.pens.ac.id dengan alamat IP 10.252.0.1, dengan waktu tempuh masing-masing 0.952 ms, 0.906 ms, dan 0.914 ms.

    Baris 6: Hop keenam menuju 124-195-38-7.resources.indosat.com dengan alamat IP 124.195.38.7, dengan waktu tempuh masing-masing 11.808 ms, 12.077 ms, dan 11.886 ms.

    Baris 7: Hop ketujuh menuju 123.108.8.172 dengan alamat IP 123.108.8.172, dengan waktu tempuh masing-masing 14.260 ms, 14.813 ms, dan 14.763 ms.

    Baris 8: Hop kedelapan mencapai tujuan dengan alamat IP 103.49.221.211 (s211-cast-211-221-49-103.detik.com) dengan waktu tempuh masing-masing 12.068 ms, 12.020 ms, dan satu kali tidak mendapatkan respons.s