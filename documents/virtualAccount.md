## Virtual account

### Create a virtual account
```java
String jsonRequest = "{\n" +
            "  \"receivers\": {\n" +
            "    \"types\": [\n" +
            "      \"bank_account\"\n" +
            "    ]\n" +
            "  },\n" +
            "  \"description\": \"Virtual Account created for Raftar Soft\",\n" +
            "  \"customer_id\": \"cust_CaVDm8eDRSXYME\",\n" +
            "  \"close_by\": 1681615838,\n" +
            "  \"notes\": {\n" +
            "    \"project_name\": \"Banking Software\"\n" +
            "  }\n" +
            "}";
              
JSONObject requestJson = new JSONObject(jsonRequest);

VirtualAccount virtualaccount = instance.virtualAccounts.create(requestJson);
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| receivers*    | object      | Array that defines what receivers are available for this Virtual Account                        |
| description  | string      | A brief description of the virtual account.                    |
| customer_id  | string      | Unique identifier of the customer to whom the virtual account must be tagged.                    |
| close_by  | integer      | UNIX timestamp at which the virtual account is scheduled to be automatically closed.                  |
| notes  | integer      | Any custom notes you might want to add to the virtual account can be entered here.                  |

**Response:**
```json
{
  "id":"va_DlGmm7jInLudH9",
  "name":"Acme Corp",
  "entity":"virtual_account",
  "status":"active",
  "description":"Virtual Account created for Raftar Soft",
  "amount_expected":null,
  "notes":{
    "project_name":"Banking Software"
  },
  "amount_paid":0,
  "customer_id":"cust_CaVDm8eDRSXYME",
  "receivers":[
    {
      "id":"ba_DlGmm9mSj8fjRM",
      "entity":"bank_account",
      "ifsc":"RATN0VAAPIS",
      "bank_name": "RBL Bank",
      "name":"Acme Corp",
      "notes":[],
      "account_number":"2223330099089860"
    }
  ],
  "close_by":1681615838,
  "closed_at":null,
  "created_at":1574837626
}
```

-------------------------------------------------------------------------------------------------------

### Create a virtual account with TPV

```java

String jsonRequest = "{\n" +
            "  \"receivers\": {\n" +
            "    \"types\": [\n" +
            "      \"bank_account\"\n" +
            "    ]\n" +
            "  },\n" +
            "  \"allowed_payers\": [\n" +
            "    {\n" +
            "      \"type\": \"bank_account\",\n" +
            "      \"bank_account\": {\n" +
            "        \"ifsc\": \"RATN0VAAPIS\",\n" +
            "        \"account_number\": 2223330027558515\n" +
            "      }\n" +
            "    }\n" +
            "  ],\n" +
            "  \"description\": \"Virtual Account created for Raftar Soft\",\n" +
            "  \"customer_id\": \"cust_HssUOFiOd2b1TJ\",\n" +
            "  \"notes\": {\n" +
            "    \"project_name\": \"Banking Software\"\n" +
            "  }\n" +
            "}";
              
JSONObject requestJson = new JSONObject(jsonRequest);

VirtualAccount virtualaccount = instance.virtualAccounts.create(requestJson);

```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| receivers*    | object      | Array that defines what receivers are available for this Virtual Account                        |
| allowed_payers*  | object      | All parameters listed [here](https://razorpay.com/docs/api/smart-collect-tpv/#create-virtual-account) are supported |
| description  | string      | A brief description of the virtual account.                    |
| customer_id  | string      | Unique identifier of the customer to whom the virtual account must be tagged.                    |
| notes  | integer      | Any custom notes you might want to add to the virtual account can be entered here.                  |

**Response:**
```json
{
  "id":"va_DlGmm7jInLudH9",
  "name":"Acme Corp",
  "entity":"virtual_account",
  "status":"active",
  "description":"Virtual Account created for Raftar Soft",
  "amount_expected":null,
  "notes":{
    "project_name":"Banking Software"
  },
  "amount_paid":0,
  "customer_id":"cust_CaVDm8eDRSXYME",
  "receivers":[
    {
      "id":"ba_DlGmm9mSj8fjRM",
      "entity":"bank_account",
      "ifsc":"RATN0VAAPIS",
      "bank_name": "RBL Bank",
      "name":"Acme Corp",
      "notes":[],
      "account_number":"2223330099089860"
    }
  ],
  "allowed_payers": [
    {
      "type": "bank_account",
      "id":"ba_DlGmm9mSj8fjRM",
      "bank_account": {
        "ifsc": "UTIB0000013",
        "account_number": "914010012345679"
      }
    },
    {
      "type": "bank_account",
      "id":"ba_Cmtnm5tSj6agUW",
      "bank_account": {
        "ifsc": "UTIB0000014",
        "account_number": "914010012345680"
      }
    }
  ],
  "close_by":1681615838,
  "closed_at":null,
  "created_at":1574837626
}
```

-------------------------------------------------------------------------------------------------------

### Create static/dynamic qr

```java
String jsonRequest = "{\n" +
            "  receivers: {\n" +
            "    types: [\n" +
            "      \"qr_code\"\n" +
            "    ]\n" +
            "  },\n" +
            "  description: \"First QR code\",\n" +
            "  amount_expected: 100,\n" +
            "  notes: {\n" +
            "    receiver_key: \"receiver_value\"\n" +
            "  }\n" +
            "}";
               
JSONObject requestJson = new JSONObject(jsonRequest);

VirtualAccount virtualaccount = instance.virtualAccounts.create(requestJson);

```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| receivers*    | array      | Array that defines what receivers are available for this Virtual Account                        |
| description  | string      | A brief description of the payment.   |
| amount_expected  | integer   | The maximum amount you expect to receive in this virtual account. Pass `69999` for ₹699.99.   |
| customer_id  | string      | Unique identifier of the customer to whom the virtual account must be tagged.                    |
| notes       | object | All keys listed [here](https://razorpay.com/docs/payments/payments/payment-methods/bharatqr/api/#create) are supported   |

**Response:**
```json
{
  "id": "va_4xbQrmEoA5WJ0G",
  "name": "Acme Corp",
  "entity": "virtual_account",
  "status": "active",
  "description": "First Payment by BharatQR",
  "amount_expected": null,
  "notes": {
    "reference_key": "reference_value"
  },
  "amount_paid": 0,
  "customer_id": "cust_805c8oBQdBGPwS",
  "receivers": [
    {
      "id": "qr_4lsdkfldlteskf",
      "entity": "qr_code",
      "reference": "AgdeP8aBgZGckl",
      "short_url": "https://rzp.io/i/PLs03pOc"
    }
  ],
  "close_by": null,
  "closed_at": null,
  "created_at": 1607938184
}
```
-------------------------------------------------------------------------------------------------------

### Fetch virtual account by id

```java
String virtualId = "va_4xbQrmEoA5WJ0G";

VirtualAccount virtualaccount = instance.virtualAccounts.fetch(virtualId);
```

**Parameters:**

| Name       | Type        | Description                                 |
|------------|-------------|---------------------------------------------|
| virtualId* | string      | The id of the virtual to be updated  |

**Response:**

For fetch virtual account by id response please click [here](https://razorpay.com/docs/api/smart-collect/#fetch-a-virtual-account-by-id)
-------------------------------------------------------------------------------------------------------

### Fetch all virtual account
```java
String jsonRequest = "{\n" +
                 "\"count\" : 1\n" +
               "}";

JSONObject requestJson = new JSONObject(jsonRequest);

List<VirtualAccount> virtualaccount = instance.virtualAccounts.fetchAll(requestJson);
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| from  | timestamp | timestamp after which the payments were created  |
| to    | timestamp | timestamp before which the payments were created |
| count | integer   | number of payments to fetch (default: 10)        |
| skip  | integer   | number of payments to be skipped (default: 0)    |

**Response:**
```json
{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "va_Di5gbNptcWV8fQ",
      "name": "Acme Corp",
      "entity": "virtual_account",
      "status": "closed",
      "description": "Virtual Account created for M/S ABC Exports",
      "amount_expected": 2300,
      "notes": {
        "material": "teakwood"
      },
      "amount_paid": 239000,
      "customer_id": "cust_DOMUFFiGdCaCUJ",
      "receivers": [
        {
          "id": "ba_Di5gbQsGn0QSz3",
          "entity": "bank_account",
          "ifsc": "RATN0VAAPIS",
          "bank_name": "RBL Bank",
          "name": "Acme Corp",
          "notes": [],
          "account_number": "1112220061746877"
        }
      ],
      "close_by": 1574427237,
      "closed_at": 1574164078,
      "created_at": 1574143517
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Fetch payments for a virtual account
```java
String virtualId = "va_DlGmm7jInLudH9";

String jsonRequest = "{\n" +
                "\"count\" : 1\n" +
               "}";

JSONObject requestJson = new JSONObject(jsonRequest);
        
List<VirtualAccount> virtualaccounts = instance.virtualAccounts.fetchPayments(virtualId,requestJson);
```

**Parameters:**

| Name       | Type      | Description                                      |
|------------|-----------|--------------------------------------------------|
| virtualId* | string    | The id of the virtual to be updated  |
| from       | timestamp | timestamp after which the payments were created  |
| to         | timestamp | timestamp before which the payments were created |
| count      | integer   | number of payments to fetch (default: 10)        |
| skip       | integer   | number of payments to be skipped (default: 0)    |

**Response:**
```json
{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "pay_Di5iqCqA1WEHq6",
      "entity": "payment",
      "amount": 239000,
      "currency": "INR",
      "status": "captured",
      "order_id": null,
      "invoice_id": null,
      "international": false,
      "method": "bank_transfer",
      "amount_refunded": 0,
      "refund_status": null,
      "captured": true,
      "description": "",
      "card_id": null,
      "bank": null,
      "wallet": null,
      "vpa": null,
      "email": "saurav.kumar@example.com",
      "contact": "+919972139994",
      "customer_id": "cust_DOMUFFiGdCaCUJ",
      "notes": [],
      "fee": 2820,
      "tax": 430,
      "error_code": null,
      "error_description": null,
      "created_at": 1574143644
    }
  ]
}
```

-------------------------------------------------------------------------------------------------------

### Fetch payment details using id and transfer method
```java
String paymentId = "pay_CmiztqmYJPtDAu";

Payment payment = instance.payments.fetchBankTransfers(paymentId)
```

**Parameters:**

| Name       | Type      | Description                         |
|------------|-----------|-------------------------------------|
| paymentId* | string    | The id of the payment to be updated |

**Response:**
```json
{
  "id": "bt_Di5iqCElVyRlCb",
  "entity": "bank_transfer",
  "payment_id": "pay_Di5iqCqA1WEHq6",
  "mode": "NEFT",
  "bank_reference": "157414364471",
  "amount": 239000,
  "payer_bank_account": {
    "id": "ba_Di5iqSxtYrTzPU",
    "entity": "bank_account",
    "ifsc": "UTIB0003198",
    "bank_name": "Axis Bank",
    "name": "Acme Corp",
    "notes": [],
    "account_number": "765432123456789"
  },
  "virtual_account_id": "va_Di5gbNptcWV8fQ",
  "virtual_account": {
    "id": "va_Di5gbNptcWV8fQ",
    "name": "Acme Corp",
    "entity": "virtual_account",
    "status": "closed",
    "description": "Virtual Account created for M/S ABC Exports",
    "amount_expected": 2300,
    "notes": {
      "material": "teakwood"
    },
    "amount_paid": 239000,
    "customer_id": "cust_DOMUFFiGdCaCUJ",
    "receivers": [
      {
        "id": "ba_Di5gbQsGn0QSz3",
        "entity": "bank_account",
        "ifsc": "RATN0VAAPIS",
        "bank_name": "RBL Bank",
        "name": "Acme Corp",
        "notes": [],
        "account_number": "1112220061746877"
      }
    ],
    "close_by": 1574427237,
    "closed_at": 1574164078,
    "created_at": 1574143517
  }
}
```
-------------------------------------------------------------------------------------------------------

### Refund payments made to a virtual account
```java
String paymentId = "pay_E54n391WnEAV9H";

String jsonRequest = "{\n" +
              "  \"amount\": \"100\",\n" +
              "  \"speed\": \"normal\",\n" +
              "  \"notes\": {\n" +
              "    \"notes_key_1\": \"Beam me up Scotty.\",\n" +
              "    \"notes_key_2\": \"Engage\"\n" +
              "  },\n" +
              "  \"receipt\": \"Receipt No. 31\"\n" +
              "}";
              
JSONObject requestJson = new JSONObject(jsonRequest);     
           
Payment payment = instance.payments.refund(paymentId,requestJson);
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| paymentId*  | string    | The id of the payment to be updated  |
|  amount       | integer      | The amount to be captured (should be equal to the authorized amount, in paise) |                       |
|  speed        | string      | Here, it must be normal                |
|  notes        | array       | A key-value pair                |
|  receipt      | string      | A unique identifier provided by you for your internal reference. |

**Response:**
```json
{
  "id": "rfnd_E6j36ZEKvsWsEn",
  "entity": "refund",
  "amount": 100,
  "currency": "INR",
  "payment_id": "pay_E54n391WnEAV9H",
  "notes": {
    "key_1": "value1",
    "key_2": "value2"
  },
  "receipt": null,
  "acquirer_data": {
    "rrn": null
  },
  "created_at": 1579522301
}
```
-------------------------------------------------------------------------------------------------------

### Add receiver to an existing virtual account
```java
String virtualId = "va_Di5gbNptcWV8fQ";

String jsonRequest = "{\n" +
                "  \"type\": [\n" +
                "    \"vpa\"\n" +
                "  ],\n" +
                "  \"vpa\": {\n" +
                "    \"descriptor\": \"gauravkumar\"\n" +
                "  }\n" +
                "}";

JSONObject requestRequest = new JSONObject(jsonRequest);

VirtualAccount virtualaccount = instance.virtualAccounts.addReceiver(virtualId,requestRequest);
```

**Parameters:**

| Name       | Type      | Description                                      |
|------------|-----------|--------------------------------------------------|
| virtualId* | string    | The id of the virtual to be updated  |
| types*     | object | The receiver type to be added to the virtual account. Possible values are `vpa` or `bank_account`  |
| vpa        | object | This is to be passed only when `vpa` is passed as the receiver types. |

**Response:**

For add receiver to an existing virtual account response please click [here](https://razorpay.com/docs/api/smart-collect/#add-receiver-to-an-existing-virtual-account)

-------------------------------------------------------------------------------------------------------

### Add an Allowed Payer Account
```java
String virtualId = "va_Di5gbNptcWV8fQ";

String jsonRequest = "{\n" +
            "  \"type\": \"bank_account\",\n" +
            "  \"bank_account\": {\n" +
            "    \"ifsc\": \"UTIB0000013\",\n" +
            "    \"account_number\": 914010012345679\n" +
            "  }\n" +
            "}";

JSONObject requestJson = new JSONObject(jsonRequest);

VirtualAccount virtualaccount = instance.virtualAccounts.addAllowedPayers(virtualId,requestJson);
```

**Parameters:**

| Name          | Type      | Description                                      |
|---------------|-----------|--------------------------------------------------|
| virtualId*    | string    | The id of the virtual to be updated  |
| type*        | object | The receiver type to be added to the virtual account. Possible values are `vpa` or `bank_account`  |
| bank_account* | object | Indicates the bank account details such as `ifsc` and `account_number` |

**Response:**
```json
{
  "id":"va_DlGmm7jInLudH9",
  "name":"Acme Corp",
  "entity":"virtual_account",
  "status":"active",
  "description":"Virtual Account created for Raftar Soft",
  "amount_expected":null,
  "notes":{
    "project_name":"Banking Software"
  },
  "amount_paid":0,
  "customer_id":"cust_CaVDm8eDRSXYME",
  "receivers":[
    {
      "id":"ba_DlGmm9mSj8fjRM",
      "entity":"bank_account",
      "ifsc":"RATN0VAAPIS",
      "bank_name": "RBL Bank",
      "name":"Acme Corp",
      "notes":[],
      "account_number":"2223330099089860"
    }
  ],
  "allowed_payers": [
    {
      "type": "bank_account",
      "id":"ba_DlGmm9mSj8fjRM",
      "bank_account": {
        "ifsc": "UTIB0000013",
        "account_number": "914010012345679"
      }
    }
  ],
  "close_by":1681615838,
  "closed_at":null,
  "created_at":1574837626
}
```
-------------------------------------------------------------------------------------------------------

### Delete an Allowed Payer Account
```java
String virtualId = "va_Di5gbNptcWV8fQ";

String allowedPlayer = "ba_DlGmm9mSj8fjRM";

VirtualAccount virtualaccount = instance.VirtualAccounts.deleteAllowedPayer(virtualId,allowedPayersId)
```

**Parameters:**

| Name             | Type      | Description                                      |
|------------------|-----------|--------------------------------------------------|
| virtualId*       | string    | The id of the virtual to be updated  |
| allowedPayersId* | string    | The id of the allowed payers to be updated  |

**Response:**
```json
null
```
-------------------------------------------------------------------------------------------------------
### Close virtual account
```java
String virtualId = "va_Di5gbNptcWV8fQ";

instance.virtualAccounts.close(virtualId)
```

**Parameters:**

| Name       | Type      | Description                                      |
|------------|-----------|--------------------------------------------------|
| virtualId* | string    | The id of the virtual to be updated  |

**Response:**

For close virtual account response please click [here](https://razorpay.com/docs/api/smart-collect/#close-a-virtual-account)
-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/smart-collect/api/)**