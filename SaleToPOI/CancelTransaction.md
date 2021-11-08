# Cancel a transaction

Sometimes your shoppers change their mind in mid-purchase, or store staff realize they've made a mistake while the shopper is using the terminal.

A cancel request lets either a shopper or store staff abort an in-progress payment. When the cancel request is received before a payment is **Approved**, the payment is cancelled.

Here we explain how you can cancel payments from your cash register

 

## Cancel from cash register

While a PaymentRequest is in progress, you can cancel it by making an AbortRequest from your cash register.

 

`MessageHeader`: The standard `SaleToPOIRequest.MessageHeader` object. This includes:

| **Parameter**     | **Required** | **Description** |
| ----------------- | ------------ | --------------- |
| `MessageClass`    | Yes          | Service         |
| `MessageCategory` | Yes          | Abort           |

`AbortRequest`: The request body with:

| **Parameter** | **Required** | **Description** |
| ------------- | ------------ | --------------- |
|               |              |                 |

| **Parameter**      | **Required** | **Description**                                              |
| ------------------ | ------------ | ------------------------------------------------------------ |
| `AbortReason`      | Yes          | `MerchantAbort`                                              |
| `MessageReference` | Yes          | An object with:`MessageCategory`: **Payment**`SaleID`: Your unique ID of the cash register that made the payment request.`ServiceID`: The `ServiceID` of the payment request being cancelled. |

 

The example below shows how you would make a request to cancel an in-progress payment with a `ServiceID` of **21796**.

```json
{
  "SaleToPOIRequest":{
    "MessageHeader":{
      "ProtocolVersion":"3.0",
      "MessageClass":"Service",
      "MessageCategory":"Abort",
      "MessageType":"Request",
      "SaleID":"POSSystemID12345",
      "ServiceID":"29239",
      "POIID":"V400m-324688179"
    },
    "AbortRequest":{
      "AbortReason":"MerchantAbort",
      "MessageReference":{
        "MessageCategory":"Payment",
        "SaleID":"POSSystemID12345",
        "ServiceID":"21796"
      }
    }
  }
}
```

The (existing) payment request returns a response containing:

1. `Result`: **Failure**
2. `ErrorCondition`: **Aborted**

If you cancelled before the shopper presented their card, the payment prompt disappears from the terminal display.
If you cancelled after the shopper presented their card, the terminal shows a **Cancelled** message.

1. To double-check the payment was indeed cancelled, make a `TransactionStatusRequest` , specifying:

   - `MessageReference`: An object with:
     - `SaleID`: The `SaleID` of the cash register that made the payment you tried to cancel.
     - `ServiceID`: The `ServiceID` of the payment you tried to cancel.
     - `MessageCategory`: **Payment**

   The example below shows how you would check the transaction status of a payment with `ServiceID` **21796**, which you tried to cancel.

```json
{
  "SaleToPOIRequest": {
    "MessageHeader": {
      "ProtocolVersion": "3.0",
      "MessageClass": "Service",
      "MessageCategory": "TransactionStatus",
      "MessageType": "Request",
      "SaleID": "POSSystemID12345",
      "ServiceID": "29240",
      "POIID": "V400m-324688179"
    },
    "TransactionStatusRequest": {
      "ReceiptReprintFlag": true,
      "DocumentQualifier": [
        "CashierReceipt",
        "CustomerReceipt"
      ],
      "MessageReference": {
        "SaleID": "POSSystemID12345",
        "ServiceID": "21796",
        "MessageCategory": "Payment"
      }
    }
  }
}
```

If the payment was cancelled, you should receive a successful  transaction status response with a RepeatedResponseMessageBody that has  an ErrorCondition of **Aborted**.

