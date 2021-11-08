# Payment Refund

## Introduction

If you want to return funds to a shopper after a payment has been Approved, you need to refund the payment.

We offer two types of refund:

- Unreferenced refund: A PaymentRequest with PaymentType Refund. Unreferenced refunds need to be manually reconciled, and let you return any amount to any card presented in-store. You can use this for example to issue a refund to someone who did not make the original payment, such as a gift recipient.
  You can implement one or both types of refund.

 

## Scope

 

Scenario 2: Refunding an offline point-of-sale payment

Scenario 3: Unreferenced Refunds

 

## Details

### Scenario 2: Make a Refund Request

## Unreferenced refunds

### Make an unreferenced refund

`MessageHeader`: The standard `SaleToPOIRequest.MessageHeader` object. This includes:

| **Parameter**   | **Required** | **Description** |
| --------------- | ------------ | --------------- |
| MessageClass    | Yes          | Service         |
| MessageCategory | Yes          | Payment         |

`PaymentRequest`: The request body with:





| **Parameter** | **Required** | **Description** |
| ------------- | ------------ | --------------- |
|               |              |                 |

| **Parameter**                   | **Required** | **Description**                                              |
| ------------------------------- | ------------ | ------------------------------------------------------------ |
| `SaleData.SaleTransactionID`    | Yes          | An object with:`TransactionID`: Your unique reference for the refund. In your Customer Area and Adyen reports, this will show as the **merchant reference**.If the original payment was an offline payment, you can make reconciliation easier by including the **tender reference of the offline payment**. `TimeStamp`: Date and time of the refund in UTC format. |
| `PaymentTransaction.AmountsReq` | Yes          | An object with:`Currency`: The transaction currency.`RequestedAmount`: The amount being refunded to the card. |
| `PaymentData.PaymentType`       | Yes          | Refund                                                       |

 

```json
{
    "SaleToPOIRequest":{
        "MessageHeader":{
            "ProtocolVersion":"3.0",
            "MessageClass":"Service",
            "MessageCategory":"Payment",
            "MessageType":"Request",
            "SaleID":"POSSystemID12345",
            "ServiceID":"12392",
            "POIID":"V400m-324688179"
        },
        "PaymentRequest":{
            "SaleData":{
                "SaleTransactionID":{
                    "TimeStamp":"2019-04-23T12:15:01+00:00",
                    "TransactionID":"YOUR_REFUND_REFERENCE"
                }
            },
            "PaymentTransaction":{
                "AmountsReq":{
                    "Currency":"EUR",
                    "RequestedAmount":10.99
                }
            },
            "PaymentData":{
                "PaymentType":"Refund"
            }
        }
    }
}
```

1. The refund request is routed to the terminal.
2. Present the card to the terminal, and follow the instructions on the terminal screen.
3. Check whether we received your refund request. If we received it:
   - **Approved** is shown on the terminal.
   - You receive a JSON response with:
     - `Result`: **Success**
     - `POIData.POITransactionID.TransactionID`: The transaction identifier for this refund request.

```json
{
    "SaleToPOIResponse": {
        "PaymentResponse": {
            "POIData": {
                "POITransactionID": {
                    "TimeStamp": "2019-06-03T15:49:36.000Z",
                    "TransactionID": "4rVu001559576976000.881559576981487A"
                },
                ...
            },
            ...
            "Response": {
                "Result": "Success",
                ...
            }
        },
        ...
    }
}
```

4. Wait for the REFUND webhook notification to learn the result.
   Refunds are always processed asynchronously. If successful, the refund is issued to the shopper's account.

 

5. [Approved] Realtime sub second.

 

6. Nothing between approved and settlement.

 

7. Very rarely some issues, very likely will be honored at some point. Sometimes the customers card is closed. Process between banks for this. These are handled out of band, between bank and merchant.