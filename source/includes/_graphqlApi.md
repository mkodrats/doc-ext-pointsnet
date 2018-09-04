# GraphQL API

Graphql API

## Pay
Query ini digunakan untuk melakukan transaksi pembayaran. Request anda harus berisi informasi berikut:
<table>
  <tr>
    <th>Field</th>
    <th>Type Data</th>
    <th>Deskripsi</th>
  </tr>
  <tr>
    <td>transaction_id</td>
    <td>String</td>
    <td>ID Transaksi</td>
  </tr>
  <tr>
    <td>points_usage</td>
    <td>Int</td>
    <td>Banyak Poin yang digunakan</td>
  </tr>
</table>

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