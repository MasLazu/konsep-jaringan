# DYNAMIC ROUTING

Routing adalah proses pengiriman data dari satu host dalam satu network ke host dalam network yang lain melalui suatu router. Agar router dapat mengetahui bagaimana meneruskan paket paket ke alamat yang dituju dengan mengunakan jalur terbaik, router menggunakan peta atau tabel routing. Table routing adalah table yang memuat seluruh informasi IP address dari interfaces router yang lain sehingga router yang satu dengan router lainnya bisa berkomunikasi.

Didalam tabel routing informasi routing akan disimpan dalam bentuk entry-entryroute (rute). Setiap entry route akan menunjukkan network address dari network yang dapat dituju oleh router tersebut. Entry route ini juga berisi tentang informasi bagaimana cara mencapai network tersebut. Entry Route pada tabel routing tersebut dapat dibuat atau dikonfigurasi secara manual oleh Administrator jaringan atau dapat juga diperoleh router secara otomatis dengan melakukan pertukaran informasi routing dengan router lain.

Seperti yang kita ketahui router berfungsi untuk mengirimkan paket data dari satu network ke network lain sekaligus menentukan jalur terbaik (best path) untuk mencapai network tujuan. Untuk menjalankan fungsi tersebut router menggunakan tabel yang disebut tabel routing (routing tabel). Tabel tersebut berisi informasi keberadaan beberapa network, baik network yang terhubung langsung (directly connected network) maupun network yang tidak terhubung langsung (remote network). 

Dalam setiap entry route juga telah ada informasi tentang interface mana yang dapat digunakan router tersebut untuk mengirimkan paket data. Jika ternyata ada entry yang cocok, maka router akan mengalihkan paket data tersebut ke interface yang dapat digunakan untuk mencapai network luar, tetapi jika ternyata tidak ada enty yang cocok, maka router akan membuang paket data tersebut. Seperti kita yang harus menggunakan pintu keberangkatan yang tepat untuk kota yang tepat pula.

Routing dinamik (dynamic routing) merupakan teknik routing dimana router akan memasukkan sendiri entry route kedalam tabel routingnya untuk melakukan itu, router akan saling bertukar informasi routing dengan router yang lain tentang jaringan yang mereka ketahui masing-masing setelah mempelajari keberadaan jaringan lain beserta cara mencapai jaringan tersebut, route akan membuat entry route dan pada akhirnya memasukkannya ke dalam tabel routing.

ntuk bisa melakukan pertukaran informasi routing, router-router tersebut harus menggunakan protokol routing jika dua buah router ingin bertukar informasi routing, maka keduanya harus menggunakan protokol routing yang sama. Berikut protokol routing yang paling banyak digunakan:
- Routing Information Protocol (RIP)
- Interior Gateway Routing Protocol (IGRP)
- Enchanced Interior Gateway Routing Protocol (EIGRP)
- Open Shortest Path First (OSPF)
- Intermediate System-to-Intermediate System (IS-IS)
- Border Gateway Protocol (BGP)

Untuk mengkonfgurasikan protokol routing pada router relatif tidak membutuhkan waktu yang lama. Kita cukup mengkonfigurasikan ip address pada setiap interface kemudian mengaktifkan protokol routing dan kemudian mengenalkan jaringan yang terhubung langsung dengan router tersebut.

Dari penjelasan diatas maka, dapat disimpulkan bahwasannya Konfigurasi Routing Dynamic (dinamik) adalah jenis routing yang bisa berubah sesuai dengan kondisi yang diinginkan dengan parameter tertentu sesuai dengan protokolnya. Dan sebuah Routing Dynamic diterapkan pada PC yang berfungsi sebagai router dan dibutuhkan router lain yang sama-sama menerapkan sistem routing dinamik, jadi tidak bisa berdiri sendiri seperti halnya Router static. Routing Dinamik juga merupakan suatu routing yang menentukan gateway untuk network destinationnya berdasarkan parameter yang didapat dari router yang lain, melalui Protokol Multicast, seperti metrik, cost dsb. Protocol RIP dan OSPF menggunakan multicast untuk pertukaran informasi antar router.

Dan bila mengkonfigurasikan router ita hanya cukup mengkonfigurasikan ip address pada setiap interface kemudian mengaktifkan protokol routing dan kemudian mengenalkan jaringan yang terhubung langsung dengan router tersebut.