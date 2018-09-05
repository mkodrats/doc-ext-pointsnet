# GraphQL API

Graphql API

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