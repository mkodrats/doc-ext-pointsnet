# HTTP(s) Request
Proses komunikasi data pada server Pointsnet dapat dilakukan melalui HTTP(s) Request. Menggunakan syarat dan ketentuan berikut :

## API Base URL
* Endpoint `https://api.pointsnet.co.uk/pointslink`

## HTTP(s) Headers

### Authorization
Pada *endpoint* (`/pointslink`) membutuhkan `Authorization` header dengan syarat dan ketentuan berikut :  

### Header

                   |                |                                                                                             |
    -------------- | -------------- | --------------------------------------------------------------------------------------------|
    Authorization: | Ganesha        | Zm9vOjhEMEM4QjdCRURFQ0NDRTM3NTAyMUM4RTAxNjQwMzkzMjZFRkJCRjcxNkY0ODkyMTM1REVENUVGQzlDMjk5OTk=|
    1              | 2              | 3                                                                                           |
    
1. Nama header
2. Nama metode otentikasi
3. Base-64 dikodekan dari `:` nilai terpisah

      |                                                                |
    --|----------------------------------------------------------------
    foo:|8D0C8B7BEDECCCE375021C8E0164039326EFBBF716F4892135DED5EFC9C29999
    a|b

   - `a`: *client token key*
   - `b`: *generated signature*

### Signature
Nilai dihitung dari HMAC SHA-256 dengan *secret key* dan *request body*.
*Secret key*  digabungkan dengan *client token key*. *Client token key* bisa anda dapatkan setelah mendaftar di Pointsnet.

### Contoh
*Secret key*: `foo`

*Request body*: `{"query": "query {transaction_detail(transaction_id: \"f64f2940-fae4-11e7-8c5f-ef356f279131\") {transaction {order_id, total_amount}, customer {first_name}} }"}`

*Generated* HMAC SHA-256: 
`8D0C8B7BEDECCCE375021C8E0164039326EFBBF716F4892135DED5EFC9C29999`

Anda dapat mencoba `HMAC Generator Online` [disini](https://www.freeformatter.com/hmac-generator.html)

   ```shell
   curl \  
   -X POST \  
   -H "Content-Type: application/json" \
   -H "Authorization: Ganesha Zm9vOjhEMEM4QjdCRURFQ0NDRTM3NTAyMUM4RTAxNjQwMzkzMjZFRkJCRjcxNkY0ODkyMTM1REVENUVGQzlDMjk5OTk=" \  
   --data '{"query": "query {transaction_detail(transaction_id: \"f64f2940-fae4-11e7-8c5f-ef356f279131\") {transaction {order_id, total_amount},customer {first_name}} }"}' \  
   https://api.pointsnet.co.uk/pointslink
   ``` 

   ```javascript
   request({     
       headers: {       
           'Content-Type': 'application/json',       
           'Authorization': 'Ganesha Zm9vOjhEMEM4QjdCRURFQ0NDRTM3NTAyMUM4RTAxNjQwMzkzMjZFRkJCRjcxNkY0ODkyMTM1REVENUVGQzlDMjk5OTk=',     
       },     
       uri: 'https://api.pointsnet.co.uk/pointslink',     
       method: 'POST',     
       body: '{"query": "query {transaction_detail(transaction_id: \"f64f2940-fae4-11e7-8c5f-ef356f279131\") {transaction {order_id, total_amount},customer {first_name}} }"}',   
    }, 
    function (err, response, body) {     
        if (! _.isNil(err)) {       
            callback(err, null);       
            return;     
        }     
        if (response.statusCode != 200) {       
            callback(body, null);       
            return;     
        }     
        let result = JSON.parse(body)     
        if (!_.isEmpty(result.errors)) {       
            var err = result.errors[0];       
            if (!_.isEmpty(err.message)) {         
                err = err.message;       
            }       
            callback(err, null);       
            return;     
        }     
        callback(null, result.data);   
    });
   ```