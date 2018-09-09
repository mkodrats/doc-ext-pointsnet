# Memulai Menggunakan API

Pointsnet memiliki dua layanan yang dapat anda gunakan untuk mulai menggunakan Pointsnet yaitu:

* Dengan menggunakan *GraphQL API* Pointsnet kedalam aplikasi yang anda bangun.
* Dengan menggunakan layanan aplikasi Pointsnet yang sudah di sediakan oleh  <a href="https://authscure.com.my/">AuthScure</a>. 

## Syarat menggunakan Pointsnet

### Mendaftarkan Aplikasi Anda

Untuk menggunakan *GraphQL API* dari Pointsnet anda harus memiliki kerja sama dengan Pointsnet untuk mendapatkan ```token``` dan ```secret key``` agar dapat mengakses sumber data dari *endpoint* yang diberikan. Untuk dapat menggunakan Pointsnet GraphQL API maupun Aplikasi Pointsnet silahkan hubungi *Call Center* pada halaman [AuthScure](https://authscure.com.my/) 

### Membuat Request

Pada *GraphQL API* Pointsnet kami menggunakan metode *request* [HTTP(s)](#http-s-request) untuk melakukan komunikasi data.

## Memulai menggunakan Pointsnet *GraphQL API*

> Contoh penggunaan query tanpa argument

```scheme
{
  hero {
    name
  }
}
```

```json
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```

> Contoh penggunaan query dengan menggunakan argument

```scheme
{
  human(id: "1234") {
    name
    height
  }
}
```

```json
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}
```

> Contoh penggunaan mutation

```scheme
  deleteHuman(id: 1234) {
    status
}
```

```json
{
  "data": {
    "deleteHuman": {
      "id": 1234,
      "alert": "Luke Skywalker successfully deleted"
    }
  }
}
```

### Diagram penggunaan Pointsnet *GraphQL API*

![gambar](pointsnetapi.png)

### Memulai menggunakan *GraphQL API*

Jika anda ingin mulai menggunakan Pointsnet kedalam aplikasi anda sendiri langkah yang harus anda pahami adalah mengenai penggunaan *GraphQL API*. Pada *GraphQL API* hanya terdapat satu *endpoint* dan terdapat dua fungsi *query* yaitu **query** dan **mutation**. 

### Query


Pada *GraphQL API query* digunakan untuk mendapatkan data dari query yang di bentuk.

### Mutation

Pada *GraphQL API mutation* digunkan untuk melakukan *posting data*.  


<aside class="success">
  Contoh dari penggunaan <i>GraphQL API query dan mutation</i> dapat anda lihat pada menu shell untuk cara penggunaan dan menu json untuk hasil. Untuk informasi dokumentasi mengenai <i>GraphQL API</i> dapat di akses pada <a href="https://graphql.org" target="_blank">https://graphql.org</a>
</aside>

### Langkah - Langkah untuk menggunakan Pointsnet *GraphQL API*

1. Langkah awal untuk dapat melakukan transaksi menggunakan Pointsnet anda diminta untuk memiliki ID Transaksi yang nantinya digunkan untuk dapat lanjut ke langkah berikutnya. Untuk mendapatkan ID Transaksi pelajari langkah [berikut](#mendapatkan-id-transaksi). ID Transaksi ini juga digunakan untuk melakukan *request* ```Proses Pembayaran```, ```Konfirmasi Data```, ```Membayar``` dan ```Rincian Transaksi```.


2. Setelah memiliki ID Transaksi langkah selanjutnya adalah melakukan *request* untuk mendapatkan daftar program (hanya program aktif) pada langkah [berikut](#daftar-program-hanya-program-aktif).

3. Setelah langkah sebelumnya dilakukan maka lakukan *request* untuk mendapatkan rincian program yang dapat anda pelajari pada langkah [berikut](#).

4. Setelah langkah diatas dilakukan maka langkah selanjutnya adalah melakukan proses pembayaran dengan menggunakan fungsi mutation dari GraphQL API dengan parameter ID Transaksi, *identification number* dan *card number*. Untuk detail lebih lanjut silahkan pelajari pada langkah [berikut](#).

5. Setelah langkah diatas berhasil maka langkah selanjutnya adalah melakukan otentifikasi kepada pengguna yang melakukan transaksi. <a href="https://authscure.com.my/">AuthScure</a> memiliki *Software as a Service (SaaS)* AuthMC yang dapat anda gunakan sebagai aplikasi yang dapat melakukan otentifikasi pada user. 

6. Setelah menyelesaikan proses otentifikasi maka langkah selanjutnya adalah melakukan konfirmasi data yang akan dibeli oleh pengguna menggunakan service Pointsnet. Langkah konfirmasi data dapat anda pelajari pada langkah [beikut](#). 

7. Setelah melakukan kofirmasi data langkah selanjutnya adalah melakukan pembayaran dengan atau tanpa tambahan cash pengguna dan dengan atau tanpa kode promosi. Ketika pengguna akan melakukan pembayaran dengan point yang cukup maka pengguna tidak akan terkena tambahan biaya pada transaksi pembayaran, tetapi apabila pengguna membeli dengan point yang kurang maka pengguna akan dikenakan biaya tambahan. Ketika pengguna melakukan pembayaran dengan menggunakan kode promosi maka sistem akan kembali melakukan konfirmasi data kembali dan memastikan kepada user bahwa point yang dimiliki ditambah dengan kode promosi tidak kurang untuk membeli barang tersebut.

8. Setelah proses pembayaran berhasil langkah selanjutnya adalah menampilkan rincian transaksi dengan menggunakan argumen yang ada pada langkah [berikut](#).


## Menggunakan Pointsnet dengan aplikasi yang di sediakan AuthScure

### Diagram penggunaan Aplikasi Pointsnet 

![gambar](apppointsnet.png)
