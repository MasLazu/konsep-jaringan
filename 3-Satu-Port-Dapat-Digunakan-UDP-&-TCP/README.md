# Alasan Satu Port Bisa Digunakan TCP dan UDP Secara Bersamaan

Sebuah soket IP (INET) memiliki identifikasi yang disebut 5-tuple, yang mencakup protokol, alamat sumber, port sumber, alamat tujuan, dan port tujuan. Konsep ini tidak terbatas hanya pada koneksi dengan sifat yang terkendali seperti TCP, tetapi juga berlaku pada berbagai jenis koneksi.

Penting untuk ditekankan bahwa protokol merupakan faktor utama yang membedakan antara koneksi-koneksi yang berbeda. Oleh karena itu, berbagai proses dapat diikat ke kombinasi unik dari 5-tuple tersebut, masing-masing dapat menggunakan protokol yang berbeda.

Secara teoretis, meskipun tidak umum dilakukan, layanan-layanan yang berbeda dapat diarahkan ke port TCP yang sama asalkan layanan-layanan tersebut terikat pada interface yang berbeda, seperti kartu jaringan yang berbeda atau interface loopback.

Walaupun UDP dan TCP adalah protokol yang berbeda, penggunaan nomor port yang sama untuk kedua protokol tersebut dapat terjadi jika tujuan komunikasi adalah layanan yang sama. Contohnya, DNS menggunakan UDP pada port 53 untuk permintaan cepat karena sifatnya yang ringan, namun juga menggunakan TCP pada port 53 untuk transfer data yang lebih besar dan lebih jarang.

Selain itu, ditekankan bahwa ada protokol lain yang dapat diimplementasikan di atas IP, dan beberapa diantaranya mungkin tidak menggunakan mekanisme perbedaan seperti port. Penjelasan ini juga menyinggung tentang adanya domain soket yang berbeda, seperti domain soket "unix", yang memiliki cara address yang berbeda dan independen dari domain soket "inet".