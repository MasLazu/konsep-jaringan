# NETWORK CONFIGURATION 6 SUBNET

<div align="center">
<img src="./assets/illustrasi.gif">
</div>

Dalam konfigurasi ini, kita menggunakan Subnet Mask /11 pada alamat IP publik 12.0.0.0/8. Ini berarti kita memiliki 2^21 = 2.097.152 alamat IP host yang tersedia dalam setiap subnet. berikut adalah konfigurasi dasarnya:

1. Router:
   * Alamat IP: 12.0.0.1/11
   * Subnet Mask: 255.224.0.0 (/11)
2. Switch 0:
   * Subnet: 12.32.0.1/11
   * PC 0 di Switch 1: 12.32.0.2/11
3. Switch 1:
   * Subnet: 12.64.0.1/11
   * PC 1 di Switch 1: 12.64.0.2/11
4. Switch 2:
   * Subnet: 12.96.0.1/11
   * PC 2 di Switch 2: 12.96.0.2/11
4. Switch 3:
   * Subnet: 12.128.0.1/11
   * PC 3 di Switch 3: 12.128.0.2/11
5. Switch 4:
   * Subnet: 12.160.0.1/11
   * PC 4 di Switch 4: 12.160.0.2/11
6. Switch 5:
   * Subnet: 12.196.0.1/11
   * PC 5 di Switch 5: 12.196.0.2/11