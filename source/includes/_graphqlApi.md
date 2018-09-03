# GraphQL API

Graphql API

## Pay
Hello this is graphql APi pay

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