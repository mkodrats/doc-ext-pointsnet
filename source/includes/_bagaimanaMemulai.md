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

API masih dalam tahap pengembangan.

## Menggunakan Aplikasi

Layanan Pointsnet dapat digunakan langsung menggunakan aplikasi yang telah disediakan oleh [Authscure](https://authscure.com.my). Pelajari bagaimana melakukan permintaan data ke server Pointsnet [disini](#http-s-request)

### Alur

![gambar](apppointsnet.png)

1. ```Frontend aplikasi klien``` melakukan *request* pada backend aplikasi klien untuk melakukan pembayaran dengan menggunakan Pointsnet.
2. ```Backend aplikasi klien``` melakukan *request create* ID transaksi pada backend Pointsnet dengan menggunakan query [Mendapatkan ID Transaksi](#mendapatkan-id-transaksi).
3. ```Backend aplikasi Pointsnet```  memberikan *response* berupa ID Transaksi pada backend aplikasi klien.
4. ```Backend aplikasi klien``` memberikan *response* URL aplikasi Pointsnet
5. ```Fronted apikasi klien``` mengalihkan ke aplikasi Pointsnet.
6. ```Aplikasi Pointsnet``` melakukan proses transaksi.
7. ```Aplikasi Pointsnet``` mengalihkan ke *backend* aplikasi klien.
8. ```Backend aplikasi klien``` melakukan cek transaksi status kepada Backend aplikasi Pointsnet.
9. ```Backend Pointsnet``` memberikan status transaksi.
10. ```Backend aplikasi klien``` memberikan respon status transaksi. 
