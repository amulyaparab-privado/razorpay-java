## Funds

### Create a fund account
```java
String jsonRequest = "{\n" +
        "  \"customer_id\":\"cust_Aa000000000001\",\n" +
        "  \"account_type\":\"bank_account\",\n" +
        "  \"bank_account\":{\n" +
        "    \"name\":\"Gaurav Kumar\",\n" +
        "    \"account_number\":\"11214311215411\",\n" +
        "    \"ifsc\":\"HDFC0000053\"\n" +
        "  }\n" +
        "}";

JSONObject requestJson = new JSONObject(jsonRequest);

FundAccount fundaccount = instance.fundAccount.create(requestJson);
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*   | string      | The id of the customer to be fetched  |
| account_type* | string      | The bank_account to be linked to the customer ID  |
| bank_account* | object      | All keys listed [here](https://razorpay.com/docs/payments/customers/customer-fund-account-api/#create-a-fund-account) are supported |

**Response:**
```json
{
  "id":"fa_Aa00000000001",
  "entity":"fund_account",
  "customer_id":"cust_Aa000000000001",
  "account_type":"bank_account",
  "bank_account":{
    "name":"Gaurav Kumar",
    "account_number":"11214311215411",
    "ifsc":"HDFC0000053",
    "bank_name":"HDFC Bank"
  },
  "active":true,
  "created_at":1543650891
}
```
-------------------------------------------------------------------------------------------------------

### Fetch all fund accounts

```java
String customerId = "cust_Aa000000000001";

FundAccount fundaccount = instance.fundAccount.fetch(customerId);
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*   | string      | The id of the customer to be fetched  |

**Response:**
```json
{
  "id":"fa_Aa00000000001",
  "entity":"fund_account",
  "customer_id":"cust_Aa000000000001",
  "account_type":"bank_account",
  "bank_account":{
    "name":"Gaurav Kumar",
    "account_number":"11214311215411",
    "ifsc":"HDFC0000053",
    "bank_name":"HDFC Bank"
  },
  "active":true,
  "created_at":1543650891
}
```
-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/payments/customers/customer-fund-account-api/)**