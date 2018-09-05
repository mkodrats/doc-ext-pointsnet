# GraphQL API

Graphql API

## Checkout
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

Query ini digunakan untuk mengirim data bank identification number atau card number agar dilakukan validasi didalam sistem.

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | Y | ID Transaksi
programme_id | String | "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea" | Y | ID Program yang dipilih
bin | Integer | 522664 | T | Merupakan Bank Identification Number yang berfungsi untuk mengidentifikasi lembaga penerbit untuk setiap akun pelanggan dan memungkinkan transaksi untuk disalurkan dengan benar.
card_number | Integer | 5226644706789205 | T | Nomor kartu pengguna

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
checkout_id | String | "8a009999-e731-4df5-b5b3-c300cb49c75d" | ID Checkout dipakai untuk melakukan validasi ke AuthMC.
redirect_uri | String | "https://example.com/redirect-uri" | Alamat uri yang akan di gunakan untuk mengalihkan ke halaman verifikasi jika menggunakan AuthMC.

## Mendapatkan detail programme
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
    "logo": "https://your-site.com/logo.png",
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
    "loyalty_code": "asdfg"
  }
```

Query ini berfungsi untuk mendapatkan detail dari program yang dipilih

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
id | String | "355675f5-1232-455a-88be-88317534a639" | Y | Ini adalah ID Program yang akan dikirim untuk mendapatkan detail programnya

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea" | Ini adalah ID dari detail program yang dipilih
name | String | "BCA BAGI BAGI" | Ini adalah nama program dari detail program yang dipilih
logo | String | "https://your-site.com/logo.png" | Ini adalah url image logo dari program yang dipilih
bank_id | String | "244f9582-b00c-11e8-96f8-529269fb1459" | Ini adalah ID bank yang mengadakan program ini
card_number_format | String | "XXXX XXXX XXXX XXXX" | Ini adalah format dari nomor kartu yang diizinkan
is_bank | Boolean | false | Ini adalah status dari program apakah yang mengadakan bank atau bukan
is_credit_card | Boolean | false | Status ini hanya boleh dimiliki oleh bank. jika is_bank bernilai true, maka field ini boleh bernilai true/false. sedangkan jika is_bank bernilai false, maka field ini otomatis bernilai false
description | String | "<p>Bank BCA bagi bagi promo point</p>" | Ini adalah deskripsi atau penjelasan dari program yang dipilih
theme_id | String | "729033a7-2ddb-4df6-bf89-8495b6337d7a" | Ini adalah ID Tema yang akan digunakan setelah melakukan pemilihan program
personnel | String | "Bank" | Ini adalah kategori dari penyedia program. misal BCA yang memiliki program maka nilainya adalah bank
lms_id | String | "5e6d71fc-b026-11e8-96f8-529269fb1459" | Ini adalah ID dari LMS
lms_name | String | "LSM" | Ini adalah nama dari LMS
bank_name | String | "BCA" | Ini adalah nama dari Bank
issuer_point | String | "10" | Ini adalah point dari penerbit
issuer_currency_code | String | "USD" | Ini adalah kode mata uang penerbit
issuer_currency_exchange | String | "10" | Ini adalah nilai tukar mata uang penerbit
point_discount_rate_percentage | String | "20" | Ini adalah nilai presentase point diskon
min_redeem_percentage | String | "30" | Ini adalah presentase minimal untuk menebus
facilitation_fee | String | "10" | Ini adalah biaya administrasi
point_cancel_fee | String | "10" | Ini adalah biaya membatalkan point
currency_cancel_fee | String | "10" | Ini adalah biaya pembatalan
is_active | Boolean | true | Ini adalah status dari detail program, apakah aktif atau tidak
loyalty_code | String | "asdfg" | Ini adalah kode loyalty

## Pay

Query ini digunakan untuk melakukan transaksi pembayaran. Request anda harus berisi informasi berikut:

```scheme
  pay (
    transaction_id: "355675f5-1232-455a-88be-88317534a639",
    points_usage: 1234,
    promo_code: "DUMY123",
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
    "currency_code": "HKD",
    "currency_rate": "1",
    "token": "183aea61-b7d0-45f3-a109-f46508cc01ef" 
  }
```

### Arguments

Field | Tipe Data | Contoh | Wajib | Deskripsi
----- | --------- | ------ | ----- | ---------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | Y | ID Transaksi
points_usage | Integer | 1234 | Y | Banyak Poin yang digunakan
promo_code | String | "DUMY123" | T | Kode Promosi   

Hasil dari request diatas akan berisi informasi berikut:

### Fields

Field | Tipe Data | Contoh    | Deskripsi
----- | --------- | --------- | -------
token | String    | "183aea61-b7d0-45f3-a109-f46508cc01ef" | ID Transaksi
cash_usage | String | "0" | Banyak uang tunai yang digunakan
currency_code | String | "HKD" | Kode mata uang
currency_rate | String | "1" | Nilai tukar mata uang
converted_cash_usage | String | "0" | Penggunaan uang tunai yang dikonversi

## Confirm
Hello this is graphql APi confirm

```scheme
confirm (
  transaction_id: "536e97e9-0d29-43ec-b8d5-a505d3ee6a8f",
  promo_code: "POINSNET123"
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

 “balance”: 120000,

 “min_redeem”: 1659,

 “max_redeem”: 19522,

 “max_slider_points”: 19540,

 “fee”: “7”,

 “point_step”: 1234,

 “point_value”: 0.0051219512195122,

 “promo_points”: 0,

 “promo_points_value”: 0,

  “message”: “ ”

}
```

| Field | Tipe Data | Contoh | Deskripsi |
| ------ | ----- | --------- | ------------ |
|transaction_id | String | "536e97e9-0d29-43ec-b8d5-a505d3ee6a8f" | ID Transaksi |
|promo_code | String | "POINSNET123" | Kode promo |
| balance | Integer | 120000 | Saldo pelanggan |
| min_redeem | Integer | 1659 | Minimal penggunaan point |
| max_redeem | Integer | 19522 | Maksimal penggunaan point |
| max_slider_points | Integer | 19540 | Maksimal point berdasarkan banyaknya point pelanggan atau hasil konversi dari total biaya ke point |
| fee | String | "7" | Biaya administrasi |
| point_step| Integer | 1234 | Nilai dari setiap step |
| point_value | Float | 0.0051219512195122 | Nilai per point |
| promo_points | Integer | 0 | Nilai point jika mengganakan promo kode |
| promo_points_value | Integer | 0 | Nilai promo point |
| message | String | "Your transaction was successful" | Pesan tentang transaksi yang berhasil/tidak |

## Mendapatkan Detail Transaksi
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
    "total_amount"  : 99.98999786376953,
    "currency"      : "HKD"
  },
  "items" :
  [ 
    { 
      "name"      : "foo",
      "category"  : "bar",
      "price"     : 99.98999786376953,
      "quantity"  : 1 
    } 
  ],
  "customer"  :
  { 
    "first_name"  : "baz",
    "last_name"   : "ban",
    "phone"       : "+6281990880318",
    "email"       : "rudy@authscure.com.my"
  },
  "expiry"        : "2018-09-30 19:24:34 +0700",
  "status"        : 1,
  "redirect_uri"  : "http://localhost",
  "programme" :
  {
    "id"                  : "23859836-cf44-6f77-a3e3-abbb455b995a",
    "name"                : "BCA BAGI BAGI",
    "logo"                : "https://your_image_logo.com",
    "card_number_format"  : "XXXX XXXX XXXX XXXX",
    "is_bank"             : false,
    "is_credit_card"      : false,
    "description"         : "Program BCA bagi-bagi"
  }, 
  "theme" :
  {
    "banner"                  : "https://your_image_banner.com",
    "card_image_front"        : "https://your_card_image_front.com",
    "card_image_back"         : "https://your_card_image_back.com",
    "card_image_logo"         : "https://your_card_image_logo.com",
    "background_color_first"  : "#FF5737",
    "background_color_second" : "#FF5733",
    "angle"                   : 360
  }
}
```

### Penjelasan
Query ini berfungsi untuk mendapatkan detail transaksi menggunkan parameter ID transaksi.

### Argumen
Untuk mendpatkan detail transaksi, query harus menyertakan parameter berupa ID transaksi seperti di bawah ini :  
**transaction_id  : "86431830-cf39-4f11-a5e5-abbb377b889a"**  
ID tersebut didapatkan ketika menjalankan query create.

Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|-------|--------|----------
transaction_id | String | "86431830-cf39-4f11-a5e5-abbb377b889a" | Y | Ini adalah ID transaksi

### Obyek

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
Transaction | [Obyek Transaction](#transaction) | Klik tipe data transaction untuk melihat field dan contoh obyek ini | Ini merupakan data-data transaksi
items | [Obyek Items](#items) | Klik isi tipe data items untuk melihat field dan contoh obyek ini | Ini merupakan data-data barang yang akan dibeli
customer | [Obyek Customer](#customer)  | Klik isi tipe data customer untuk melihat field dan contoh obyek ini | Ini merupakan data-data pelanggan yang sedang melakukan transaksi
expiry | String | "2018-09-30 19:24:34 +0700" | Ini adalah masa berlaku dari ID transaksi
status | Integer | 1 | Ini adalah status hasil request ID transaksi. 0 = Berhasil, 1 = Tertunda, 2 = Gagal
redirect_uri | String | "http://localhost" | Ini adalah url yang akan dibuka ketika request transaksi berhasil
programme | [Obyek Programme](#programme) | Klik isi tipe data programme untuk melihat field dan contoh obyek ini | Ini merupakan data-data program yang dipilih
theme | [Obyek Theme](#theme) | Klik isi tipe data theme untuk melihat field dan contoh obyek ini | Ini merupakan data-data tema

### Transaction
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
order_id | String | "86431830-cf39-4f11-a5e5-abbb377b889a" | Ini adalah ID order transaksi yang sedang dilakukan
total_amount | Float | 99.98999786376953 | Ini adalah total harga item yang akan dibeli
currency | String | "HKD" | Ini adalah jenis mata uang yang digunakan
[Kembali ke daftar obyek](#obyek)
### Items
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
name | String | "foo" | Ini adalah nama barang yang akan dibeli
category | String | "bar" | Ini adalah kategori barang yang akan dibeli
price | Float | 99.98999786376953 | Ini adalah harga barang yang akan dibeli
quantity | Integer | 1 | Ini adalah jumlah barang yang akan dibeli
[Kembali ke daftar obyek](#obyek)
### Customer
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
first_name | String | "baz" | Ini adalah nama depan pelanggan yang sedang melakukan transaksi ini
last_name | String | "ban" | Ini adalah nama belakang pelanggan yang sedang melakukan transaksi ini
phone | String | "+6281990880318" | Ini adalah nomor telepon pelanggan yang sedang melakukan transaksi ini
email | String | "rudy@authscure.com.my" | Ini adalah alamat email pelanggan yang sedang melakukan transaksi ini  
[Kembali ke daftar obyek](#obyek)
### Programme
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "23859836-cf44-6f77-a3e3-abbb455b995a" | Ini adalah ID dari program yang dipilih
name | String | "BCA BAGI BAGI" | Ini adalah nama dari program yang dipilih
logo | String | "https://your_image_logo.com" | Ini adalah URL logo dari program yang dipilih
card_number_format | String | "XXXX XXXX XXXX XXXX" | Ini adalah format nomor kartu kredit dari program yang dipilih
is_bank | Boolean | false | Jika nilai adalah "true" maka adalah bank, jika nilai adalah "false" maka bukan bank
is_credit_card | Boolean | false | Jika nilai adalah "true" maka adalah kartu kredit, jika nilai adalah "false" maka bukan kartu kredit
description | String | "Program BCA bagi-bagi" | Ini adalah deskripsi dari program yang dipilih
[Kembali ke daftar obyek](#obyek)
### Theme
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
banner | String | "https://your_image_banner.com" | Ini adalah url gambar banner
card_image_front | String | "https://your_image_front.com" | Ini adalah url gambar tampak depan kartu kredit
card_image_back | String | "https://your_image_back.com" | Ini adalah url gambar tampak belakang kartu kredit
card_image_logo | String | "https://your_image_banner.com" | Ini adalah url gambar logo
background_color_first | String | "#FF5737" | Ini adalah kode warna latar pertama
background_color_first | String | "#FF5733" | Ini adalah kode warna latar kedua
angle | Integer | 360 | Ini adalah nilai derajat dari tata letak tema
[Kembali ke daftar obyek](#obyek)

## Daftar Program (Hanya program aktif)
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
    "description"        : "Bank BCA bagi bagi promo point",
    "id"                 : "a02fd8bb-b6c0-4bbe-bcbb-9045a2b974ea",
    "is_bank"            : true,
    "logo"               : "https://2.bp.blogspot.com/-_BITDWSaNos/WKggIVMUczI/AAAAAAAAB4g/d5-te8J3Ahos89_RQf0UkbTXKOQVQHDRwCPcB/s1600/Logo%2BBank%2BBCA_PNG.png",
    "name"               : "BCA BAGI BAGI" 
  },
  { 
    "card_number_format" : "XXXX XXXX XXXX XXXX",
    "description"        : "<p>Dummy programme for admin id</p>",
    "id"                 : "d2971e38-5236-4656-822c-c6440916c5a8",
    "is_bank"            : false,
    "logo"               : "https://media.licdn.com/dms/image/C510BAQGvQkJ994tLwA/company-logo_200_200/0?e=1543449600&v=beta&t=Pc43SWEhxP7fst1WFZbvfoQjC3W7uPJVwDC0801KgWM",
    "name"               : "Admin Programme" 
  }
 ]
```

### Penjelasan
Query ini berfungsi untuk menampilkan daftar program yang aktif.

### Argumen
Field | Tipe Data | Contoh | Wajib | Deskripsi
------|-----------|--------|-------|----------
active_only | Boolean | true | Y | Menampilkan daftar program yang aktif. active_only bernilai true apabila program berstatus aktif dan active_only bernilai false apabila program berstatus tidak aktif.

Hasil dari request diatas akan berisi informasi seperti berikut:

### Fields
Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
id | String | "d2971e38-5236-4656-822c-c6440916c5a8" | ID dari program yang ditawarkan.
name | String | "Dummy programme" | Nama dari program yang ditawarkan.
logo | String | "https://your_image_logo.com" | URL logo dari *merchant* yang menawarkan program.
card_number_format | String | "XXXX XXXX XXXX XXXX" | Format penulisan nomor kartu kredit.
is_bank | Boolean | false | Status *merchant* ( bank atau non bank). is_bank bernilai true apabila program ditawarkan dari *merchant* bank dan is_bank bernilai false apabila program ditawarkan dari *merchant* non bank.
description | String | "Admin Programme" | Deskripsi dari program yang ditawarkan.

## Mendapatkan ID Transaksi

### Penjelasan

Query ini digunakan untuk mendapatkan ID Transaksi

```scheme
  create (
    transaction: {
      order_id: "123",
      total_amount: 0.14,
      currency: "MYR"
    },
    items: [{
      name: "foo",
      category: "bar",
      price: 250.0,
      quantity: 1,
    }],
    customer: {
      first_name: "baz",
      last_name: "ban",
      email: "foo.bar@baz.ban",
      phone: "+1234",
    },
    expiry: {
      start_time: "2006-01-02T15:04:05+07:00",
      unit: "minute",
      duration: 5,
    }
    ) {
    transaction_id
        }
  }
```

```json
  { 
      "transaction_id": "355675f5-1232-455a-88be-88317534a639"
  }
```
### Arguments

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
transaction  | [Obyek Transaction](#transaction) | Klik tipe data transaction untuk melihat field dan contoh obyek ini | Objek yang menyimpan informasi transaction.  
items        | [Obyek Transaction](#items)       | Klik tipe data transaction untuk melihat field dan contoh obyek ini | Objek yang menyimpan informasi items.
customer     | [Obyek Transaction](#customer)    | Klik tipe data transaction untuk melihat field dan contoh obyek ini | Objek yang menyimpan informasi items.
expiry       | [Obyek Transaction](#expiry)      | Klik tipe data transaction untuk melihat field dan contoh obyek ini | Objek yang menyimpan informasi items.

### Expiry

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
start_time | String  | "2006-01-02T15:04:05+07:00" | Ini adalah masa berlaku dari ID transaksi
unit       | String  | "minute" | Ini adalah satuan unit yang digunakan untuk menentukan waktu
duration   | Integer | 5 | Ini adalah durasi waktu 

### Fields

Field | Tipe Data | Contoh | Deskripsi
------|-----------|--------|----------
transaction_id | String | "355675f5-1232-455a-88be-88317534a639" | ID Transaksi 
