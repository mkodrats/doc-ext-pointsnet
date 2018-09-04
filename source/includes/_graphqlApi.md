# GraphQL API

Graphql API

## Pay

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

Query ini digunakan untuk melakukan transaksi pembayaran. Request anda harus berisi informasi berikut:

### Arguments


Field | Tipe Data | Contoh | Wajib | Deskripsi
----- | --------- | ------ | ----- | ---------
transaction_id | String | 355675f5-1232-455a-88be-88317534a639 | Y | ID Transaksi
points_usage | Int | 1234 | Y | Banyak Poin yang digunakan
promo_code | String | DUMY123 | T | Kode Promosi   

Hasil dari request diatas akan berisi informasi berikut:

### Fields

Field | Tipe Data | Contoh    | Deskripsi
----- | --------- | --------- | -------
token | String    | 183aea61-b7d0-45f3-a109-f46508cc01ef | ID Transaksi
cash_usage | String | 0 | Banyak uang tunai yang digunakan
currency_code | String | HKD | Kode mata uang
currency_rate | String | 1 | Nilai tukar mata uang
converted_cash_usage | String | 0 | Penggunaan uang tunai yang dikonversi



## Confirm

```scheme
confirm (
  transaction_id: $id,
  promo_code: $promoCode
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