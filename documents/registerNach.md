## Register nach and charge first payment together

### Create customer
```java
String jsonRequest = "{\n" +
            "  \"name\": \"Gaurav Kumar\",\n" +
            "  \"contact\": 9123456780,\n" +
            "  \"email\": \"gaurav.kumar@example.com\",\n" +
            "  \"fail_existing\": 0,\n" +
            "  \"gstin\": \"29XAbbA4369J1PA\",\n" +
            "  \"notes\": {\n" +
            "    \"notes_key_1\": \"Tea, Earl Grey, Hot\",\n" +
            "    \"notes_key_2\": \"Tea, Earl Grey… decaf.\"\n" +
            "  }\n" +
            "}";
              
JSONObject requestJson = new JSONObject(jsonRequest);   
          
Customer customer = instance.customers.create(requestJson);
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| name*          | string      | Name of the customer                        |
| email        | string      | Email of the customer                       |
| contact      | string      | Contact number of the customer              |
| fail_existing | string | If a customer with the same details already exists, the request throws an exception by default. Possible value is `0` or `1`|
| notes         | object      | A key-value pair                            |

**Response:**
```json
{
  "id": "cust_1Aa00000000003",
  "entity": "customer",
  "name": "Gaurav Kumar",
  "email": "Gaurav.Kumar@example.com",
  "contact": "9000000000",
  "gstin": null,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "created_at": 1582033731
}
```
-------------------------------------------------------------------------------------------------------

### Create Order

```java
String jsonRequest = "{\n" +
        "  \"amount\": 100,\n" +
        "  \"currency\": \"INR\",\n" +
        "  \"method\": \"nach\",\n" +
        "  \"receipt\": \"Receipt No. 5\",\n" +
        "  \"notes\": {\n" +
        "    \"note_key 1\"\": \"Beam me up Scotty\",\n" +
        "    \"note_key 2\"\": \"Tea. Earl Gray. Hot.\"\n" +
        "  },\n" +
        "  \"token\": {\n" +
        "    \"first_payment_amount\": 10000,\n" +
        "    \"auth_type\": \"physical\",\n" +
        "    \"max_amount\": 50000,\n" +
        "    \"expire_at\": 1634215992,\n" +
        "    \"notes\": {\n" +
        "      \"note_key 1\": \"Tea, Earl Grey… decaf.\",\n" +
        "      \"note_key 2\": \"Tea. Earl Gray. Hot.\"\n" +
        "    },\n" +
        "    \"bank_account\": {\n" +
        "      \"beneficiary_name\": \"Gaurav Kumar\",\n" +
        "      \"account_number\": 11214311215411,\n" +
        "      \"account_type\": \"savings\",\n" +
        "      \"ifsc_code\": \"HDFC0001233\"\n" +
        "    },\n" +
        "    \"nach\": {\n" +
        "      \"form_reference1\": \"Recurring Payment for Gaurav Kumar\",\n" +
        "      \"form_reference2\": \"Method Paper NACH\",\n" +
        "      \"description\": \"Paper NACH Gaurav Kumar\"\n" +
        "    }\n" +
        "  }\n" +
        "}";

JSONObject requestRequest = new JSONObject(jsonRequest);

Order order = instance.orders.create(requestRequest);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| method*      | string  | Payment method used to make the registration transaction. Possible value is `nach`.  |
| receipt      | string  | Your system order reference id.  |
| token.auth_type*  | string  | Possible value is `physical`|
| token.max_amount  | integer  | Use to set the maximum amount per debit request. The value can range from `500` - `1000000000` (1cr, default value)  |
| token.expire_at  | integer | The timestamp, in Unix format, till when the  registration link should expire |
| token.notes  | object  | A key-value pair  |
| bank.account_number*  | string  | Customer's bank account number.  |
| bank.ifsc_code*  | string  | Customer's bank IFSC  |
| bank.beneficiary_name*  | string  |  Customer's name  |
| bank.account_type*  | string  | Customer's bank account. Possible value is `saving`(default), `current`, `cc`, `nre`, `nro`  |
| nach.form_reference1  | string  | A user-entered reference that appears on the NACH form  |
| nach.form_reference2  | string  | A user-entered reference that appears on the NACH form  |
| nach.description  | string  | All keys listed  |
| notes | object  | A key-value pair  |

**Response:**
```json
{
  "id":"order_1Aa00000000001",
  "entity":"order",
  "amount":0,
  "amount_paid":0,
  "amount_due":0,
  "currency":"INR",
  "receipt":"rcptid #10",
  "offer_id":null,
  "offers":{
    "entity":"collection",
    "count":0,
    "items":[]
  },
  "status":"created",
  "attempts":0,
  "notes": {
    "notes_key_1": "Beam me up Scotty",
    "notes_key_2": "Engage"
  },
  "created_at":1579775420,
  "token":{
    "method":"nach",
    "notes": {
      "notes_key_1": "Tea, Earl Grey, Hot",
      "notes_key_2": "Tea, Earl Grey… decaf."
    },
    "recurring_status":null,
    "failure_reason":null,
    "currency":"INR",
    "max_amount":10000000,
    "auth_type":"physical",
    "expire_at":1580480689,
    "nach":{
      "create_form":true,
      "form_reference1":"Recurring Payment for Gaurav Kumar",
      "form_reference2":"Method Paper NACH",
      "prefilled_form":"https://rzp.io/i/bitw",
      "upload_form_url":"https://rzp.io/i/gts",
      "description":"Paper NACH Gaurav Kumar"
    },
    "bank_account":{
      "ifsc":"HDFC0000001",
      "bank_name":"HDFC Bank",
      "name":"Gaurav Kumar",
      "account_number":"11214311215411",
      "account_type":"savings",
      "beneficiary_email":"gaurav.kumar@example.com",
      "beneficiary_mobile":"9876543210"
    },
    "first_payment_amount":10000
  }
}
```
-------------------------------------------------------------------------------------------------------

### Create an Authorization Payment

Please refer this [doc](https://razorpay.com/docs/api/recurring-payments/paper-nach/auto-debit/#113-create-an-authorization-payment) for authorization payment

-----------------------------------------------------------------------------------------------------

### Create registration link

```java
String jsonRequest = "{\n" +
        "  \"customer\": {\n" +
        "    \"name\": \"Gaurav Kumar\",\n" +
        "    \"email\": \"gaurav.kumar@example.com\",\n" +
        "    \"contact\": 9123456780\n" +
        "  },\n" +
        "  \"amount\": 0,\n" +
        "  \"currency\": \"INR\",\n" +
        "  \"type\": \"link\",\n" +
        "  \"description\": \"12 p.m. Meals\",\n" +
        "  \"subscription_registration\": {\n" +
        "    \"method\": \"nach\",\n" +
        "    \"auth_type\": \"physical\",\n" +
        "    \"bank_account\": {\n" +
        "      \"beneficiary_name\": \"Gaurav Kumar\",\n" +
        "      \"account_number\": 11214311215411,\n" +
        "      \"account_type\": \"savings\",\n" +
        "      \"ifsc_code\": \"HDFC0001233\"\n" +
        "    },\n" +
        "    \"nach\": {\n" +
        "      \"form_reference1\": \"Recurring Payment for Gaurav Kumar\",\n" +
        "      \"form_reference2\": \"Method Paper NACH\"\n" +
        "    },\n" +
        "    \"expire_at\": 1947483647,\n" +
        "    \"max_amount\": 50000\n" +
        "  },\n" +
        "  \"receipt\": \"Receipt No. 1\",\n" +
        "  \"sms_notify\": 1,\n" +
        "  \"email_notify\": 1,\n" +
        "  \"expire_by\": 1647483647,\n" +
        "  \"notes\": {\n" +
        "    \"note_key 1\": \"Beam me up Scotty\",\n" +
        "    \"note_key 2\": \"Tea. Earl Gray. Hot.\"\n" +
        "  }\n" +
        "}";

        JSONObject requestRequest = new JSONObject(jsonRequest);

        Invoice invoice = instance.invoices.createRegistrationLink(requestRequest);
```

**Parameters:**

| Name            | Type    | Description                                                   |
|-----------------|---------|---------------------------------------------------------------|
| customer   | object      | Details of the customer to whom the registration link will be sent. |
| type*  | object | the value is `link`. |
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| description*  | string      | A brief description of the payment.   |
| subscription_registration   | object  | All keys listed [here](https://razorpay.com/docs/api/recurring-payments/paper-nach/auto-debit/#121-create-a-registration-link) are supported  |
| receipt      | string  | Your system order reference id.  |
| sms_notify  | boolean  | SMS notifications are to be sent by Razorpay (default : 1)  |
| email_notify | boolean  | Email notifications are to be sent by Razorpay (default : 1)  |
| expire_by    | integer | The timestamp, in Unix format, till when the customer can make the authorization payment. |
| notes | object  | A key-value pair  |

**Response:**
```json
{
    "id": "inv_FHrZiAubEzDdaq",
    "entity": "invoice",
    "receipt": "Receipt No. 27",
    "invoice_number": "Receipt No. 27",
    "customer_id": "cust_BMB3EwbqnqZ2EI",
    "customer_details": {
        "id": "cust_BMB3EwbqnqZ2EI",
        "name": "Gaurav Kumar",
        "email": "gaurav.kumar@example.com",
        "contact": "9123456780",
        "gstin": null,
        "billing_address": null,
        "shipping_address": null,
        "customer_name": "Gaurav Kumar",
        "customer_email": "gaurav.kumar@example.com",
        "customer_contact": "9123456780"
    },
    "order_id": "order_FHrZiBOkWHZPOp",
    "line_items": [],
    "payment_id": null,
    "status": "issued",
    "expire_by": 1647483647,
    "issued_at": 1595491154,
    "paid_at": null,
    "cancelled_at": null,
    "expired_at": null,
    "sms_status": "sent",
    "email_status": "sent",
    "date": 1595491154,
    "terms": null,
    "partial_payment": false,
    "gross_amount": 0,
    "tax_amount": 0,
    "taxable_amount": 0,
    "amount": 0,
    "amount_paid": 0,
    "amount_due": 0,
    "currency": "INR",
    "currency_symbol": "₹",
    "description": "12 p.m. Meals",
    "notes": {
        "note_key 1": "Beam me up Scotty",
        "note_key 2": "Tea. Earl Gray. Hot."
    },
    "comment": null,
    "short_url": "https://rzp.io/i/bzDYbNg",
    "view_less": true,
    "billing_start": null,
    "billing_end": null,
    "type": "link",
    "group_taxes_discounts": false,
    "created_at": 1595491154,
    "idempotency_key": null,
    "token": {
        "method": "nach",
        "notes": {
            "note_key 1": "Beam me up Scotty",
            "note_key 2": "Tea. Earl Gray. Hot."
        },
        "recurring_status": null,
        "failure_reason": null,
        "currency": "INR",
        "max_amount": 50000,
        "auth_type": "physical",
        "expire_at": 1947483647,
        "nach": {
            "create_form": true,
            "form_reference1": "Recurring Payment for Gaurav Kumar",
            "form_reference2": "Method Paper NACH",
            "prefilled_form": "https://rzp.io/i/exdIzYN",
            "upload_form_url": "https://rzp.io/i/bzDYbNg",
            "description": "12 p.m. Meals"
        },
        "bank_account": {
            "ifsc": "HDFC0001233",
            "bank_name": "HDFC Bank",
            "name": "Gaurav Kumar",
            "account_number": "11214311215411",
            "account_type": "savings",
            "beneficiary_email": "gaurav.kumar@example.com",
            "beneficiary_mobile": "9123456780"
        },
        "first_payment_amount": 0
    },
    "nach_form_url": "https://rzp.io/i/exdIzYN"
}
```
-------------------------------------------------------------------------------------------------------

## Create an order to charge the customer

```java
String jsonRequest = "{\n" +
              "  \"amount\": \"100\",\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"receipt\": \"Receipt No. 1\",\n" +
              "  \"notes\": {\n" +
              "    \"key1\": \"value3\",\n" +
              "    \"key2\": \"value2\"\n" +
              "  }\n" +
              "}";
              
JSONObject requestRequest = new JSONObject(jsonRequest);         
       
Order order = instance.orders.create(requestRequest);
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| receipt      | string  | Your system order reference id.  |
| payment_capture  | boolean  | Indicates whether payment status should be changed to captured automatically or not. Possible values: true - Payments are captured automatically. false - Payments are not captured automatically. |
| notes | object  | A key-value pair  |

**Response:**
```json
{
   "id":"order_1Aa00000000002",
   "entity":"order",
   "amount":1000,
   "amount_paid":0,
   "amount_due":1000,
   "currency":"INR",
   "receipt":"Receipt No. 1",
   "offer_id":null,
   "status":"created",
   "attempts":0,
   "notes":{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey… decaf."
   },
   "created_at":1579782776
}
```
-------------------------------------------------------------------------------------------------------

## Create a recurring payment

```java
String jsonRequest = "{\n" +
              "  \"email\": \"gaurav.kumar@example.com\",\n" +
              "  \"contact\": \"9123456789\",\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"order_id\": \"order_1Aa00000000002\",\n" +
              "  \"customer_id\": \"cust_1Aa00000000001\",\n" +
              "  \"token_id\": \"token_1Aa00000000001\",\n" +
              "  \"recurring\": \"1\",\n" +
              "  \"description\": \"Creating recurring payment for Gaurav Kumar\",\n" +
              "  \"notes\": {\n" +
              "    \"note_key 1\": \"Beam me up Scotty\",\n" +
              "    \"note_key 2\": \"Tea. Earl Gray. Hot.\"\n" +
              "  }\n" +
              "}";
  
JSONObject requestJson = new JSONObject(jsonRequest);  
              
Payment payment = instance.payments.createRecurringPayment(requestJson);
```
**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| email*   | string      | The customer's email address |
| contact*   | string      | The customer's phone number |
| amount*   | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency*   | string  | The currency of the payment (defaults to INR)  |
| orderId*   | string      | The id of the order to be fetched |
| customerId*   | string      | The id of the customer to be fetched |
| tokenId*   | string      | The id of the token to be fetched |
| recurring*   | boolean      | Possible values is `0` or `1` |
| description  | string      | A brief description of the payment.   |
| notes | object  | A key-value pair  |

**Response:**
```json
{
  "razorpay_payment_id" : "pay_1Aa00000000001",
  "razorpay_order_id" : "order_1Aa00000000001",
  "razorpay_signature" : "9ef4dffbfd84f1318f6739a3ce19f9d85851857ae648f114332d8401e0949a3d"
}
```
-------------------------------------------------------------------------------------------------------

## Send/Resend notifications

```java
String invoiceId = "inv_DAweOiQ7amIUVd";

String medium = "sms";

Invoice invoice = instance.invoices.notifyBy(invoiceId,medium);
```
**Parameters:**

| Name       | Type    |Description      |
|------------|---------|------------------------------------------------------------------------------|
| invoiceId* | string      | The id of the invoice to be fetched |
| medium*    | string      | Possible values are `sms` or `email` |

**Response:**
```json
{
    "success": true
}
```

-------------------------------------------------------------------------------------------------------

## Cancel registration link

```java
String invoiceId = "inv_DAweOiQ7amIUVd";

Invoice invoice = instance.invoices.cancel(invoiceId);
```
**Parameters:**

| Name       | Type    | Description                                                                  |
|------------|---------|------------------------------------------------------------------------------|
| invoiceId* | string      | The id of the invoice to be fetched |

**Response:**
```json
{
  "id": "inv_FHrZiAubEzDdaq",
  "entity": "invoice",
  "receipt": "Receipt No. 27",
  "invoice_number": "Receipt No. 27",
  "customer_id": "cust_BMB3EwbqnqZ2EI",
  "customer_details": {
    "id": "cust_BMB3EwbqnqZ2EI",
    "name": "Gaurav Kumar",
    "email": "gaurav.kumar@example.com",
    "contact": "9123456780",
    "gstin": null,
    "billing_address": null,
    "shipping_address": null,
    "customer_name": "Gaurav Kumar",
    "customer_email": "gaurav.kumar@example.com",
    "customer_contact": "9123456780"
  },
  "order_id": "order_FHrZiBOkWHZPOp",
  "line_items": [],
  "payment_id": null,
  "status": "cancelled",
  "expire_by": 1647483647,
  "issued_at": 1595491154,
  "paid_at": null,
  "cancelled_at": 1595491339,
  "expired_at": null,
  "sms_status": "sent",
  "email_status": "sent",
  "date": 1595491154,
  "terms": null,
  "partial_payment": false,
  "gross_amount": 0,
  "tax_amount": 0,
  "taxable_amount": 0,
  "amount": 0,
  "amount_paid": 0,
  "amount_due": 0,
  "currency": "INR",
  "currency_symbol": "₹",
  "description": "12 p.m. Meals",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "comment": null,
  "short_url": "https://rzp.io/i/bzDYbNg",
  "view_less": true,
  "billing_start": null,
  "billing_end": null,
  "type": "link",
  "group_taxes_discounts": false,
  "created_at": 1595491154,
  "idempotency_key": null,
  "token": {
    "method": "nach",
    "notes": {
      "note_key 1": "Beam me up Scotty",
      "note_key 2": "Tea. Earl Gray. Hot."
    },
    "recurring_status": null,
    "failure_reason": null,
    "currency": "INR",
    "max_amount": 50000,
    "auth_type": "physical",
    "expire_at": 1947483647,
    "nach": {
      "create_form": true,
      "form_reference1": "Recurring Payment for Gaurav Kumar",
      "form_reference2": "Method Paper NACH",
      "prefilled_form": "https://rzp.io/i/tSYd5aV",
      "upload_form_url": "https://rzp.io/i/bzDYbNg",
      "description": "12 p.m. Meals"
    },
    "bank_account": {
      "ifsc": "HDFC0001233",
      "bank_name": "HDFC Bank",
      "name": "Gaurav Kumar",
      "account_number": "11214311215411",
      "account_type": "savings",
      "beneficiary_email": "gaurav.kumar@example.com",
      "beneficiary_mobile": "9123456780"
    },
    "first_payment_amount": 0
  },
  "nach_form_url": "https://rzp.io/i/tSYd5aV"
}
```
-------------------------------------------------------------------------------------------------------

## Fetch token by payment id

```java
String paymentId = "pay_1Aa00000000001";

Payment payment = instance.payments.fetch(paymentId);
```
**Parameters:**

| Name       | Type    | Description                                                                  |
|------------|---------|------------------------------------------------------------------------------|
| paymentId* | string  | The id of the payment to be fetched |

**Response:**
```json
{
  "id": "pay_EnLNTjINiPkMEZ",
  "entity": "payment",
  "amount": 0,
  "currency": "INR",
  "status": "captured",
  "order_id": "order_EnLLfglmKksr4K",
  "invoice_id": "inv_EnLLfgCzRfcMuh",
  "international": false,
  "method": "nach",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": true,
  "description": "Invoice #inv_EnLLfgCzRfcMuh",
  "card_id": null,
  "bank": "UTIB",
  "wallet": null,
  "vpa": null,
  "email": "gaurav.kumar@example.com",
  "contact": "+919876543210",
  "customer_id": "cust_DtHaBuooGHTuyZ",
  "token_id": "token_EnLNTnn7uyRg5V",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "fee": 0,
  "tax": 0,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {},
  "created_at": 1588827564
}
```
-------------------------------------------------------------------------------------------------------

## Fetch tokens by customer id

```java
String customerId = "cust_BMB3EwbqnqZ2EI";

List<Token> token = instance.customers.fetchTokens(customerId);
```
**Parameters:**

| Name        | Type    | Description                                                                  |
|-------------|---------|------------------------------------------------------------------------------|
| CustomerId* | string      | The id of the customer to be fetched |

**Response:**
```json
{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "token_EhYgIE3pOyMQpD",
      "entity": "token",
      "token": "3mQ5Czc6APNppI",
      "bank": "HDFC",
      "wallet": null,
      "method": "nach",
      "vpa": null,
      "recurring": true,
      "recurring_details": {
        "status": "confirmed",
        "failure_reason": null
      },
      "auth_type": "physical",
      "mrn": null,
      "used_at": 1587564373,
      "created_at": 1587564373,
      "dcc_enabled": false
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

## Delete tokens

```java
String customerId = "cust_BMB3EwbqnqZ2EI";

String tokenId = "token_FHf94Uym9tdYFJ";

Customer customer = instance.customers.deleteToken(customerId, tokenId);
```
**Parameters:**

| Name        | Type    | Description                                                                  |
|-------------|---------|------------------------------------------------------------------------------|
| CustomerId* | string      | The id of the customer to be fetched |
| TokenId*    | string      | The id of the token to be fetched |

**Response:**
```json
{
    "deleted": true
}
```
-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/recurring-payments/paper-nach/auto-debit/)**