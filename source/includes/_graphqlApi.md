# GraphQL API

## Mendapatkan ID Transaksi

```scheme
  create (
    transaction: {
      order_id: "123",
      total_amount: 0.14,
      currency: "MYR"
    },
    items: [
      {
        name: "foo",
        category: "bar",
        price: 250.0,
        quantity: 1,
      }
    ],
    customer: {
      first_name: "baz",
      last_name: "ban",
      email: "email@example.com",
      phone: "+6282 XXX XXX XXX",
    },
    expiry: {
      start_time: "2006-01-02T15:04:05+07:00",
      unit: "minute",
      duration: 5,
    }
  ){
    transaction_id
   }
```

```json
  { 
    "transaction_id": "355675f5-1232-455a-88be-88317534a639"
  }
```

### Penjelasan

Query ini digunakan untuk mendapatkan ID Transaksi

### Arguments

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
transaction  | [Transaction](#transaction) | Klik *Transaction* untuk melihat *field* | Objek yang menyimpan informasi transaksi.
items        | [][Items](#items)     | Klik *Items* untuk melihat obyek | Objek yang menyimpan informasi *field*.
customer     | [Customer](#customer)    | Klik *Customer* untuk melihat *field* | Objek yang menyimpan informasi *Customer*.
expiry       | [Expiry](#expiry)      | Klik *Expiry* untuk melihat *field* | Objek yang menyimpan informasi *Expiry*.

### Expiry

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
start_time | String  | "2006-01-02T15:04:05+07:00" | Masa berlaku dari ID transaksi
unit       | String  | "minute" | Satuan unit yang digunakan untuk menentukan waktu
duration   | Integer | 5 | Durasi waktu 

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | ID Transaksi menggunakan format UUID


## Daftar program (Hanya program aktif)
```scheme
  programme_list (
    active_only: true
  ) {
    id,
    name,
    logo,
    card_number_format,
    is_bank,
    description
  }
```

```json
[
  { 
    "card_number_format" : "XXXX XXXX XXXX XXXX",
    "description"        : "Bagi bagi point kepada pelanggan setia",
    "id"                 : "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea",
    "is_bank"            : true,
    "logo"               : "https://example.com/logo.png",
    "name"               : "Pointnet Programme" 
  },
  { 
    "card_number_format" : "XXXX XXXX XXXX XXXX",
    "description"        : "<p>Dummy programme for admin id</p>",
    "id"                 : "d2971e38-5236-4656-822c-c6440916c5a8",
    "is_bank"            : false,
    "logo"               : "https://example.com/logo.png",
    "name"               : "Dummy programme" 
  }
 ]
```

### Penjelasan

Query ini berfungsi untuk menampilkan daftar program yang aktif.

### Arguments
Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
active_only | Boolean | true | Y | `active_only` bernilai `true` akan menampilkan semua program yang berstatus aktif dan `active_only` bernilai `false` akan menampilkan semua program termasuk yang tidak aktif.

Hasil dari *request* diatas akan berisi informasi seperti berikut:

### Fields
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "d2971e38-5236-4656-822c-c6440916c5a8" | ID dari program yang ditawarkan dan menggunakan format UUID.
name | String | "Dummy programme" | Nama dari program yang ditawarkan.
logo | String | "https://your_image_logo.com" | URL logo dari *merchant* yang menawarkan program.
card_number_format | String | "XXXX XXXX XXXX XXXX" | Format penulisan nomor kartu kredit.
is_bank | Boolean | false | Status *merchant* ( bank atau non bank). `is_bank` bernilai `true` apabila program ditawarkan dari *merchant* bank dan is_bank bernilai `false` apabila program ditawarkan dari *merchant* non bank.
description | String | "Admin Programme" | Deskripsi dari program yang ditawarkan.






## Rincian program

```scheme
  programme_detail(
    id: "355675f5-1232-455a-88be-88317534a639"
  ) {
    id
    name
    logo
    bank_id
    card_number_format
    is_bank
    is_credit_card
    description
    theme_id
    personnel
    lms_id
    lms_name
    bank_name
    issuer_point
    issuer_currency_code
    issuer_currency_exchange
    point_discount_rate_percentage
    min_redeem_percentage
    facilitation_fee
    point_cancel_fee
    currency_cancel_fee
    is_active
    loyalty_code
  }
```

```json
  {
    "id": "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea",
    "name": "BCA BAGI BAGI",
    "logo": "https://example.com/logo.png",
    "bank_id": "244f9582-b00c-11e8-96f8-529269fb1459",
    "card_number_format": "XXXX XXXX XXXX XXXX",
    "is_bank": false,
    "is_credit_card": false,
    "description": "<p>Bank BCA bagi bagi promo point</p>",
    "theme_id": "729033a7-2ddb-4df6-bf89-8495b6337d7a",
    "personnel": "Bank",
    "lms_id": "5e6d71fc-b026-11e8-96f8-529269fb1459",
    "lms_name": "LMS",
    "bank_name": "BCA",
    "issuer_point": "10",
    "issuer_currency_code": "USD",
    "issuer_currency_exchange": "10",
    "point_discount_rate_percentage": "20",
    "min_redeem_percentage": "30",
    "facilitation_fee": "10",
    "point_cancel_fee": "10",
    "currency_cancel_fee": "10",
    "is_active": true,
    "loyalty_code": "MOCK"
  }
```
### Penjelasan
Query ini berfungsi untuk mendapatkan rincian dari program yang dipilih

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
id | String | "355675f5-1232-455a-88be-88317534a639" | Y | ID Program yang akan dikirim untuk mendapatkan rincian programnya dan menggunakan format UUID

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea" | ID dari program yang dipilih dan menggunakan format UUID
name | String | "BCA BAGI BAGI" | Nama dari rincian program yang dipilih
logo | String | "https://your-site.com/logo.png" | *Url image* logo dari program yang dipilih
bank_id | String | "244f9582-b00c-11e8-96f8-529269fb1459" | ID bank yang bekerja sama dengan program dan menggunakan format UUID
card_number_format | String | "XXXX XXXX XXXX XXXX" | Format dari nomor kartu yang diizinkan
is_bank | Boolean | false | Status dari program apakah yang mengadakan bank atau bukan
is_credit_card | Boolean | false | Status ini hanya dapat dimiliki oleh bank. Jika `is_bank` bernilai `true`, maka *field* ini boleh bernilai `true`/`false`. Jika `is_bank` bernilai `false`, maka *field* ini otomatis bernilai `false`
description | String | "<p>Bank BCA bagi bagi promo point</p>" | Deskripsi atau penjelasan dari program yang dipilih
theme_id | String | "729033a7-2ddb-4df6-bf89-8495b6337d7a" | ID Tema program, yang akan digunakan untuk keperluan pengambilan tema program
personnel | String | "Bank" | Kategori dari penyedia program. Misal BCA yang memiliki program maka nilainya adalah Bank
lms_id | String | "5e6d71fc-b026-11e8-96f8-529269fb1459" | ID LMS menggunakan format UUID
lms_name | String | "LMS" | Nama LMS
bank_name | String | "BCA" | Nama Bank
issuer_point | String | "10" | Point penerbit
issuer_currency_code | String | "USD" | Kode mata uang penerbit
issuer_currency_exchange | String | "10" | Nilai tukar mata uang penerbit
point_discount_rate_percentage | String | "20" | Nilai presentase *point* diskon
min_redeem_percentage | String | "30" | Persentase minimal untuk menebus
facilitation_fee | String | "10" | Biaya administrasi
point_cancel_fee | String | "10" | Biaya pembatalan transaksi
currency_cancel_fee | String | "10" | Biaya pembatalan transaksi dalam satuan uang
is_active | Boolean | true | Status dari rincian program, apakah aktif atau tidak
loyalty_code | String | "MOCK" | Kode *loyalty*

## Proses pembayaran
```scheme
  checkout (
    transaction_id: "355675f5-1232-455a-88be-88317534a639",
    programme_id: "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea",
    bin: 522664,
    card_number: 5226644706789205
  ) {
    checkout_id
    redirect_uri
  }
```

```json
  {
    "checkout_id": "8a009999-e731-4df5-b5b3-c300cb49c75d",
    "redirect_uri": "https://example.com/redirect-uri"
  }
```

### Penjelasan

Query ini digunakan untuk mengirim data bank *identification number* atau *card number* agar dilakukan validasi didalam sistem untuk melanjutkan pembayaran.

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | Y | ID Transaksi menggunakan format UUID
programme_id | String | "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea" | Y | ID Program yang dipilih dan menggunakan format UUID
bin | Integer | 522664 | T | *Bank Identification Number* yang berfungsi untuk mengidentifikasi lembaga penerbit untuk setiap akun pelanggan dan memungkinkan transaksi untuk disalurkan dengan benar.
card_number | Integer | 5226644706789205 | T | Nomor kartu pengguna

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
checkout_id | String | "8a009999-e731-4df5-b5b3-c300cb49c75d" | ID *Checkout* dipakai untuk melakukan validasi ke AuthMC dan menggunakan format UUID.
redirect_uri | String | "https://example.com/redirect-uri" | Alamat uri yang akan di gunakan untuk mengalihkan ke halaman verifikasi jika menggunakan AuthMC.



## Konfirmasi data

```scheme
confirm (
  transaction_id: "536e97e9-0d29-43ec-b8d5-a505d3ee6a8f",
  promo_code: "APRILASYIK"
) {
  balance 
  min_redeem
  max_redeem
  max_slider_points
  fee
  point_step
  point_value
  promo_points
  promo_points_value
  message
}
```

```json
{
 "balance": 120000,
 "min_redeem": 1659,
 "max_redeem": 19522,
 "max_slider_points": 19540,
 "fee": "7",
 "point_step": 1234,
 "point_value": 0.0051219512195122,
 "promo_points": 0,
 "promo_points_value": 0,
 "message": ""
}
```

### Penjelasan
Query ini di gunakan untuk melakukan konfirmasi data sebelum melakukan melakukan pembayaran. dimana dengan menjalankan query ini anda akan mendapatkan informasi berupa data seperti pada tabel *field*.

### Arguments
Untuk mendapatkan informasi data, query harus menyertakan parameter berupa ID transaksi atau kode promo seperti di bawah ini :  


 Field | Tipe Data | Contoh | Wajib | Deskripsi |
| ------ | ----- | --------- | ------- | ------------ |
|transaction_id | String | "536e97e9-0d29-43ec-b8d5-a505d3ee6a8f" | Y | ID Transaksi menggunakan format UUID |
|promo_code | String | "APRILASYIK" | T | Kode promo |

### Fields

| Field | Tipe Data | Contoh | Deskripsi |
| ------ | ----- | --------- | ------------ |
| balance | Integer | 120000 | Saldo pelanggan |
| min_redeem | Integer | 1659 | Minimal penggunaan *point* |
| max_redeem | Integer | 19522 | Maksimal penggunaan *point* |
| max_slider_points | Integer | 19540 | Maksimal *point* berdasarkan banyaknya *point* pelanggan atau hasil konversi dari total biaya ke *point* |
| fee | String | "7" | Biaya administrasi |
| point_step| Integer | 1234 | Nilai dari setiap step |
| point_value | Float | 0.0051219512195122 | Nilai per *point* |
| promo_points | Integer | 0 | Nilai *point* jika mengganakan promo kode |
| promo_points_value | Integer | 0 | Nilai promo point |
| message | String | "Your transaction was successful" | Pesan tentang transaksi yang berhasil/tidak |

## Membayar

```scheme
  pay (
    transaction_id: "355675f5-1232-455a-88be-88317534a639",
    points_usage: 1234,
    promo_code: "HEMAT100",
  ) {
    token
    cash_usage
    currency_code
    currency_rate
    converted_cash_usage
  }
```

```json
  { 
    "cash_usage": "0",
    "converted_cash_usage": "0",
    "currency_code": "MYR",
    "currency_rate": "1",
    "token": "183aea61-b7d0-45f3-a109-f46508cc01ef" 
  }
```
### Penjalasan

Query ini digunakan untuk melakukan transaksi pembayaran. *Request* anda harus berisi informasi berikut:

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
----- | --------- | ------ | ----- | ---------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | Y | ID Transaksi menggunakan format UUID
points_usage | Integer | 1234 | Y | Banyak Poin yang digunakan
promo_code | String | "HEMAT100" | T | Kode Promosi   

Hasil dari request diatas akan berisi informasi berikut:

### Fields

Field | Tipe Data | Contoh    | Deskripsi
----- | --------- | --------- | -------
token | String    | "183aea61-b7d0-45f3-a109-f46508cc01ef" | ID Transaksi menggunakan format UUID
cash_usage | String | "0" | Banyak uang tunai yang digunakan
currency_code | String | "MYR" | Kode mata uang
currency_rate | String | "1" | Nilai tukar mata uang
converted_cash_usage | String | "0" | Penggunaan uang tunai yang dikonversi

## Rincian transaksi
```scheme
transaction_detail (
  transaction_id: "86431830-cf39-4f11-a5e5-abbb377b889a"
) 
{
  transaction {
    order_id,
    total_amount,
    currency,
  },
  items{
    name,
    category,
    price,
    quantity,
  },
  customer{
    first_name,
    last_name,
    phone,
    email,
  },
  expiry,
  status,
  redirect_uri,
  programme{
    id,
    name,
    logo,
    card_number_format,
    is_bank,
    is_credit_card,
    description
  },
  theme{
    banner,
    card_image_front,
    card_image_back,
    card_image_logo,
    background_color_first,
    background_color_second,
    angle
  }
}
```

```json
{ 
  "transaction" :
  { 
    "order_id"      : "ORDER_123",
    "total_amount"  : 99.98,
    "currency"      : "MYR"
  },
  "items" :
  [ 
    { 
      "name"      : "foo",
      "category"  : "bar",
      "price"     : 99.98,
      "quantity"  : 1 
    } 
  ],
  "customer"  :
  { 
    "first_name"  : "baz",
    "last_name"   : "ban",
    "phone"       : "+6282 XXX XXX XXX",
    "email"       : "email@example.com"
  },
  "programme" :
  {
    "id"                  : "23859836-cf44-6f77-a3e3-abbb455b995a",
    "name"                : "BCA BAGI BAGI",
    "logo"                : "https://example.com/logo.com",
    "card_number_format"  : "XXXX XXXX XXXX XXXX",
    "is_bank"             : false,
    "is_credit_card"      : false,
    "description"         : "Program BCA bagi-bagi"
  }, 
  "theme" :
  {
    "banner"                  : "https://example.com/your_image_banner.png",
    "card_image_front"        : "https://example.com/your_card_image_front.png",
    "card_image_back"         : "https://example.com/your_card_image_back.png",
    "card_image_logo"         : "https://example.com/your_card_image_logo.png",
    "background_color_first"  : "#FF5737",
    "background_color_second" : "#FF5733",
    "angle"                   : 360
  },
  "expiry"        : "2018-09-30 19:24:34 +0700",
  "status"        : 1,
  "redirect_uri"  : "http://example.com",
}
```

### Penjelasan
Query ini berfungsi untuk mendapatkan rincian transaksi menggunkan parameter ID transaksi.

### Arguments
Untuk mendapatkan rincian transaksi, query harus menyertakan parameter berupa ID transaksi seperti di bawah ini :  

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|-------|--------|----------
transaction_id | String | "86431830-cf39-4f11-a5e5-abbb377b889a" | Y | ID transaksi menggunakan format UUID

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
Transaction | Transaction | Klik *Transaction* untuk melihat *field* | Informasi transaksi
items | []Items | Klik *Items* untuk melihat *field* | Data pembelian oleh pelanggan.
customer | Customer  | Klik *Customer* untuk melihat *field* | Informasi data pelanggan.
programme | Programme | Klik *Programme* untuk melihat *field* | Informasi data program yang dipilih
theme | Theme | Klik *Theme* untuk melihat *field* | Informasi data tema.
expiry | String | "2018-09-30T19:24:34 +0700" | Masa berlaku ID transaksi.
status | Integer | 1 | Status hasil *request* ID transaksi. 0 = Berhasil, 1 = Tertunda, 2 = Gagal
redirect_uri | String | "http://localhost" | Url yang akan dibuka ketika *request* transaksi berhasil.

### Transaction
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
order_id | String | "1253236" | ID Order dari transaksi
total_amount | Float | 99.98 | Total harga item yang akan dibeli
currency | String | "MYR" | Jenis mata uang yang digunakan

### Items
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
name | String | "foo" | Nama barang yang dibeli
category | String | "bar" | Kategori barang yang dibeli
price | Float | 99.98 | Harga barang yang dibeli
quantity | Integer | 1 | Jumlah barang yang dibeli

### Customer
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
first_name | String | "baz" | Nama depan pelanggan yang sedang melakukan transaksi
last_name | String | "ban" | Nama belakang pelanggan yang sedang melakukan transaksi
phone | String | "+6282 XXX XXX XXX" | Nomor telepon pelanggan yang sedang melakukan transaksi
email | String | "email@example.com" | Alamat email pelanggan yang sedang melakukan transaksi

### Programme
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "23859836-cf44-6f77-a3e3-abbb455b995a" | ID program yang dipilih dan menggunakan format UUID
name | String | "BCA BAGI BAGI" | Nama program yang dipilih
logo | String | "https://example.com/your_image_logo.png" | URL logo dari program yang dipilih
card_number_format | String | "XXXX XXXX XXXX XXXX" | Format nomor kartu kredit dari program yang dipilih
is_bank | Boolean | false | Apabila `is_bank` bernilai `true` maka identifikasi untuk bank, jika nilai adalah `false` maka identifikasi selain bank
is_credit_card | Boolean | false | Jika nilai adalah `true` maka identifikasi untuk kartu kredit, jika nilai adalah `false` maka identifikasi selain kartu kredit
description | String | "Program BCA bagi-bagi" | Deskripsi program yang dipilih

### Theme
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
banner | String | "https://example.com/your_image_banner.png" | Url gambar banner
card_image_front | String | "https://example.com/your_image_front.png" | Url gambar tampak depan kartu kredit
card_image_back | String | "https://example.com/your_image_back.png" | Url gambar tampak belakang kartu kredit
card_image_logo | String | "https://example.com/your_image_logo.png" | Url gambar logo
background_color_first | String | "#FF5737" | Kode warna latar pertama
background_color_first | String | "#FF5733" | Kode warna latar kedua
angle | Integer | 360 | Nilai derajat dari tata letak tema
