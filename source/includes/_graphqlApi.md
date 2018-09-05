# GraphQL API

Graphql API

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