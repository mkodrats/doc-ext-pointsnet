# Mulai

Pointsnet merupakan layanan yang menggabungkan `point` dari loyalty yang berkerja sama dengan `Pointsnet`. dengan point pengguna dapat melakukan transaksi pembayaran ke semua layanan yang bekerjasama dengan pointsnet.

Pointsnet menawarkan dua pilihan dalam menghubungkan ke aplikasi anda, yaitu

 - Mengembangkan sendiri di sisi aplikasi anda menggunakan API yang di sediakan. [dokumentasi](#menggunakan-api)
 - Menggunakan metode redirect ke Aplikasi Pointsnet yang sudah di sediakan oleh [AuthScure](https://authscure.com.my). [dokumentasi](#menggunakan-aplikasi)

### Memulai menggunakan *GraphQL API*

Jika anda ingin mulai menggunakan Pointsnet kedalam aplikasi anda langkah yang harus anda pahami adalah mengenai penggunaan *GraphQL API*. Pada *GraphQL API* hanya terdapat satu *endpoint* dan terdapat dua fungsi *query* yaitu **query** dan **mutation**.

<aside class="success">
  Untuk informasi dokumentasi mengenai <i>GraphQL API</i> dapat di akses pada <a href="https://graphql.org" target="_blank">https://graphql.org</a>
</aside>

## Persyaratan
 
 Wajib memiliki `token` dan `sekret key`

 Untuk mendapatkan `token` dan `sekret key` silahkan hubungi [AuthScure](https://authscure.com.my)

## Menggunakan API

API ini disediakan oleh Poinstnet untuk di kembangkan disisi Aplikasi anda. Pelajari bagaimana melakukan permintaan data ke server Pointsnet [disini](#http-s-request)

### Alur

![gambar](pointsnetapi.png)



### Langkah - Langkah untuk menggunakan Pointsnet *GraphQL API*

1. Langkah awal untuk dapat melakukan transaksi menggunakan Pointsnet anda diminta untuk memiliki ID Transaksi yang nantinya digunkan untuk dapat lanjut ke langkah berikutnya. Untuk mendapatkan ID Transaksi pelajari langkah [berikut](#mendapatkan-id-transaksi). ID Transaksi ini juga digunakan untuk melakukan *request* ```Proses Pembayaran```, ```Konfirmasi Data```, ```Membayar``` dan ```Rincian Transaksi```.


2. Setelah memiliki ID Transaksi langkah selanjutnya adalah melakukan *request* untuk mendapatkan daftar program (hanya program aktif) pada langkah [berikut](#daftar-program-hanya-program-aktif).

3. Setelah langkah sebelumnya dilakukan maka lakukan *request* untuk mendapatkan rincian program yang dapat anda pelajari pada langkah [berikut](#).

4. Setelah langkah diatas dilakukan maka langkah selanjutnya adalah melakukan proses pembayaran dengan menggunakan fungsi mutation dari GraphQL API dengan parameter ID Transaksi, *identification number* dan *card number*. Untuk detail lebih lanjut silahkan pelajari pada langkah [berikut](#).

5. Setelah langkah diatas berhasil maka langkah selanjutnya adalah melakukan otentifikasi kepada pengguna yang melakukan transaksi. <a href="https://authscure.com.my/">AuthScure</a> memiliki *Software as a Service (SaaS)* AuthMC yang dapat anda gunakan sebagai aplikasi yang dapat melakukan otentifikasi pada user. 

6. Setelah menyelesaikan proses otentifikasi maka langkah selanjutnya adalah melakukan konfirmasi data yang akan dibeli oleh pengguna menggunakan service Pointsnet. Langkah konfirmasi data dapat anda pelajari pada langkah [beikut](#). 

7. Setelah melakukan kofirmasi data langkah selanjutnya adalah melakukan pembayaran dengan atau tanpa tambahan cash pengguna dan dengan atau tanpa kode promosi. Ketika pengguna akan melakukan pembayaran dengan point yang cukup maka pengguna tidak akan terkena tambahan biaya pada transaksi pembayaran, tetapi apabila pengguna membeli dengan point yang kurang maka pengguna akan dikenakan biaya tambahan. Ketika pengguna melakukan pembayaran dengan menggunakan kode promosi maka sistem akan kembali melakukan konfirmasi data kembali dan memastikan kepada user bahwa point yang dimiliki ditambah dengan kode promosi tidak kurang untuk membeli barang tersebut.

8. Setelah proses pembayaran berhasil langkah selanjutnya adalah menampilkan rincian transaksi dengan menggunakan argumen yang ada pada langkah [berikut](#).


## Menggunakan Aplikasi

### Diagram penggunaan Aplikasi Pointsnet 

![gambar](apppointsnet.png)
