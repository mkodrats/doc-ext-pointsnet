# GraphQL API

Graphql API

## Pay
Query ini digunakan untuk melakukan transaksi pembayaran. Request anda harus berisi informasi berikut:

Field | Type Data | Deskripsi
----- | --------- | ---------
transaction_id | String | ID Transaksi
points_usage | Int | Banyak Poin yang digunakan


Hasil dari request diatas akan berisi informasi berikut:

Field | Type Data | Deskripsi
----- | --------- | ---------
token | String | ID Transaksi
cash_usage | Int | Banyak uang tunai yang digunakan
currency_code | Int | Kode mata uang
currency_rate | Int | Nilai tukar mata uang
converted_cash_usage | Int | Penggunaan uang tunai yang dikonversi

```scheme
  pay (
    transaction_id: $id,
    points_usage: $pointsUsage,
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
    token
    cash_usage
    currency_code
    currency_rate
    converted_cash_usage
  }
```

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